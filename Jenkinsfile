pipeline {
  agent none
  stages {
    stage('Server') {
      parallel {
        stage('Server') {
          steps {
            sh '''echo " building server"
mvn --version
mkdir -p target
touch "target/server.war"'''
            stash(name: 'Server', includes: '**/*.war')
          }
        }

        stage('Client') {
          steps {
            sh '''echo "building the client"
npm install --save react
mkdir -p dist
cat > dist/index.html <<EOF
hello!
EOF
touch "dist/client.js"'''
            stash(name: 'Client', includes: '**/dist/*')
          }
        }

      }
    }

    stage('Test_Docker') {
      steps {
        sh 'docker ps -a'
      }
    }

  }
  environment {
    docker = ''
  }
}