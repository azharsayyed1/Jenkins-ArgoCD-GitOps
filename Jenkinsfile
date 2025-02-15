pipeline {
    agent any

    stages {
        stage('Checkout GitHub') {
            steps {
                git(
                    branch: 'main', 
                    credentialsId: 'githubID', 
                    url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps.git'
                )
            }
        }
    }
}
