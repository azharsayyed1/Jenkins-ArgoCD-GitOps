pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    environment{
        DOCKER_HUB_REPO= 'azharsayyed1222/jenkins-argocd-gitops' 
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'gitops', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps'
            }
        }

        stage('NPM install') {  // Fixed incorrect stage declaration
            steps {
                sh 'npm install'
            }
        }

        stage('Build docker file'){
            steps{
                echo 'Installing docker file'
                docker.Build("${DOCKER_HUB_REPO"}:latest")
            }
        }

    }
}
