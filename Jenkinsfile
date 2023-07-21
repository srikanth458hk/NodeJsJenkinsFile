@Library('pullRequest') _
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
               
              script {
                    sh './build.sh'
                    def pullRequestId = sh(returnStdout: true, script: 'echo $CHANGE_ID').trim()
                    storePullRequestInfo(pullRequestId)
                }
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
    
    
   
