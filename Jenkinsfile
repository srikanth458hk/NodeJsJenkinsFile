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
                    def jenkinsUrl = 'http://jenkins-server:8080' // Replace with your Jenkins server URL
                    
                    // Trigger the infrastructure pipeline
                    def response = httpRequest(
                        url: "${jenkinsUrl}/job/${infraJobName}/build",
                        method: 'POST',
                        authentication: 'usernamePassword',
                        username: 'srikanth', // Replace with your Jenkins username
                        password: '11458@Hk'  // Replace with your Jenkins password or API token
                    )
                    
                    if (response.status != 201) {
                        error("Failed to trigger the infrastructure pipeline. Response status: ${response.status}")
                    }
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
    
    
   
