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

        stage{
            stage('NPM install'){
                steps{
                        sh 'npm install'
                }
            }
        }
    }
}
}
