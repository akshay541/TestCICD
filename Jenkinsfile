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
        git url:'https://github.com/akshay541/TestCICD.git', branch:'main'
      }
    }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("akshay541/node:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', '3705f38d-6e84-41f5-824c-1e86e0f8b109') {
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
