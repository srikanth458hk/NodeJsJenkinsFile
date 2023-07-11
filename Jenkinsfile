pipeline {
  agent any

   stages {
     
     stage('Fetch Scripts') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url:'https://github.com/srikanth458hk/nodejsrepo.git']]])

                sh 'chmod +x build.sh push.sh deploy.sh'
            }
        }

        stage('Build') {
            steps {
                sh './build.sh'
            }
        }
     stage('Test') {
       steps {

          sh 'npm test'

       }
     }

        stage('Push') {
            steps {
                sh './push.sh'
            }
        }
     stage('Deploy')
     {
     steps {
       sh './deploy.sh'
    }
}


   }
}
    
    
   
