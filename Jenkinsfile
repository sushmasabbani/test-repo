pipeline {
    agent any

    stages {
        stage('Checkout') {   # Cloning the source code from github respository using credentialsID
            steps {
                git url: 'https://github.com/sushmasabbani/test-repo.git', branch: 'main', credentialsId: 'gitaccess'
            }
        }
        stage('Build image') { # Building the docker image using the dockerfile 
            steps {
                script {
      	              sh 'docker build -t test/test-image:latest .' 
                }
            }    
        }
        stage('Deploy app') {  # Deploying and Exposing the app to internet using kubernetes ingress
            steps {
                script {
                      sh 'kubectl --kubeconfig=/home/ec2-user/.kube/k8s-config apply -f test-ingress.yaml'
                      sh 'kubectl --kubeconfig=/home/ec2-user/.kube/k8s-config apply -f test.yaml'
                }
            }
        }
   }
}
