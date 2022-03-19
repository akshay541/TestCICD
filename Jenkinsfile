 pipeline {
 	agent any
	 environment {
       registry = "magalixcorp/k8scicd"
       GOCACHE = "/tmp"
   }
  stages {
        stage('Git Checkout') {
            steps {
                echo 'Checkout/Pull Code from Github'
                step([$class: 'WsCleanup'])
                checkout([
	                $class: 'GitSCM', 
	                branches: [[name: 'main']],  
	                userRemoteConfigs: [[credentialsId: '7b912c8e-dbda-4ec3-a58b-9d4b72826fd7', url: 'git@github.com:tejprakashbkn/TestCICD']]
	                ])
	           sh "ls -l"
                
            }
        }
        stage('Build') {
		tools {
        go 'go-1.11'
    }
    environment {
        GO111MODULE = 'on'
    }
           
            steps {
                sh 'go build'
            }
        
 }
 }
 }
