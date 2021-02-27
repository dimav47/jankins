pipeline {

  agent {

    docker {
      image 'dimav47/buildtools'
      args  '-v /var/run/docker.sock:/var/run/docker.sock -u 0:0'
      registryCredentialsId 'fdb54f96-c857-4a66-b6e2-fc0e8064b437'
    }
  }
  
  stages {
      
      stage('Git clone') {
        steps {
          git 'https://github.com/dimav47/boxfuse12.git'
        }
      }
      
      stage('Build') {
        steps {
          sh 'mvn package'
          }
      }
      
      stage('Build and push docker image') {
        steps {
          sh 'docker build -f Dockerfile -t dimav47/prodtoweb:web .'
          sh 'docker push dimav47/prodtoweb:web'
          }
      }
      
      stage('Docker pull and run webapp') {
        steps {
          sshagent(['d7d98222-05d1-4c52-a766-b7568507d350']) {
            sh '''ssh -o StrictHostKeyChecking=no root@34.123.37.68 << EOF
            docker pull dimav47/prodtoweb:web
            docker run --rm --name prod-webapp-deployed -d -p 8888:8080 dimav47/prodtoweb:web
EOF'''
        }
      }
    }
      }
  }