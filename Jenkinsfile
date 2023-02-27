pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Kwill76/learn-terraform-provision-eks-cluster.git'
            }
        }
        
        stage('Terraform Apply') {
            steps {
                withAWS(credentials: 'aws-creds') {
                    sh 'terraform init'
                    sh 'terraform apply -auto-approve'
                }
            }
        }
        
        stage('Configure Kubernetes') {
            steps {
                sh 'kubectl apply -f kubernetes-config.yml'
            }
        }
        
        stage('Deploy Application') {
            steps {
                sh 'kubectl apply -f app-deployment.yml'
            }
        }
    }
}
