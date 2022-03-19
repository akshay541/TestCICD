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
            agent {
               docker {
                   image 'golang'
               }
           }
           steps {
               // Create our project directory.
               sh 'cd ${GOPATH}/src'
               sh 'mkdir -p ${GOPATH}/src/hello-world'
               // Copy all files in our Jenkins workspace to our project directory.
               sh 'cp -r ${WORKSPACE}/* ${GOPATH}/src/hello-world'
               // Build the app.
	       sh 'cd ${GOPATH}/src/hello-world'	   
	       sh 'go mod init'
	       sh 'go mod tidy'  
               sh 'go build'
           }
 }
 }
 }
