pipeline {
    agent any
    environment {
        PROJECT_ID = 'PROJECT-ID'
        CLUSTER_NAME = 'CLUSTER-NAME'
        LOCATION = 'CLUSTER-LOCATION'
        CREDENTIALS_ID = 'gke'
    }
    stages {
        stage('Checkout Source') {
      steps {
        git url:'https://github.com/tejprakashbkn/TestCICD.git', branch:'main'
      }
    }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("tejprakashbkn/node:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
        stage('Deploy to App') {
            steps {
        script {
          //kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "mykubeconfig")
          sh 'sed -i \'s/BUILDNUMBER/\'$BUILD_ID\'/g\' deployment.yml'
          sh 'cat deployment.yml'
          sh 'kubectl apply -f deployment.yml'
        }
      }
        }
    }    
}
