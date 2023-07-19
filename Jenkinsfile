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
       stage('Trigger Infrastructure Pipeline') {
            steps {
                script {
                    def infraJobName = 'infrajob' // Name of your infrastructure pipeline job
                    
                    // Trigger the infrastructure pipeline
                    build job: "${infraJobName}", wait: false
                }
            }
        }

        stage('Build') {
            steps {
                sh './build.sh'
            }
        }
     
        stage('Push') {
          
            steps {
                sh './push.sh'
            }
        }
     stage('Deploy')
     {
       input {
         message 'Do you want to process with the deployment?'
         ok "Deploy"
       }
     steps {
       sh './deploy.sh'
    }
}
     

   }
}
    
    
   
