 pipeline {
 agent any
   environment {
       REPO_URL = "git@github.com:tejprakashbkn/TestCICD"
       GOCACHE = "/tmp"
       GIT_CRED_ID = "7b912c8e-dbda-4ec3-a58b-9d4b72826fd7"
   }
  stages {
        stage('Git Checkout') {
            steps {
                echo 'Checkout/Pull Code from Github'
                step([$class: 'WsCleanup'])
                checkout([
	                $class: 'GitSCM', 
	                branches: [[name: 'main']],  
	                userRemoteConfigs: [[credentialsId: GIT_CRED_ID, url: REPO_URL]]
	                ])
	           sh "ls -l"
                
            }
        }
 }
 }
