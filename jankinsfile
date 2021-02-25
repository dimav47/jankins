pipeline {

  agent {

    docker {
      image 'dimav47/buildtools'
      args  '-v /var/run/docker.sock:/var/run/docker.sock -u 0:0'
      
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
     
      
      
      }
  }
