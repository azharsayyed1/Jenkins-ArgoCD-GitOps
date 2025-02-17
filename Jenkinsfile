pipeline {
    agent any
    tools {
        nodejs 'NodeJS' // Ensure NodeJS is configured in Jenkins
    }
    environment {
        DOCKER_HUB_REPO = 'azharsayyed1222/jenkins-argocd-gitops'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'gitops', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps'
            }
        }
        stage('NPM Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }
        stage('Trivy Scan for Image'){
            steps{
           		
                sh 'trivy --severity HIGH,CRITICAL --skip-update --no-progress image --format table -o trivy-scan-report.txt ${DOCKER_HUB_REPO}:latest'
                
  
            }
        }
    }
}
