pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                
                  git branch: 'main', credentialsId: 'jenkinsfinish', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps.git'  
            }
        }
     
    }
}
