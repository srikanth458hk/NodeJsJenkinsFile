pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'chmod +x build.sh'
        sh './build.sh'
      }
    }
    stage('Push') {
      steps {
        
        sh 'chmod +x push.sh'
        sh './push.sh'

      }
    }
    
    
   
  }
}
