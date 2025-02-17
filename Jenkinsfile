pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
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
    }
}
