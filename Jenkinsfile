pipeline {
    agent any
    tools {
        nodejs 'NodeJS' // Ensure NodeJS is configured in Jenkins
    }
    environment {
        DOCKER_HUB_REPO = 'azharsayyed1222/jenkins-argocd-gitops'
        DOCKER_HUB_CREDENTIALS_ID = 'gitops-dockerhub'
    }
    stages {
        stage('Checkout') {
            steps {
//                git branch: 'main', credentialsId: 'gitops', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps'
                  git branch: 'main', credentialsId: 'jenkinsfinish', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps.git'  
            }
        }
        stage('NPM Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Docker ') {
            steps {
                script {
                    dockerImage=docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }

        stage('pushing image to dockerhub'){
            steps{
                script{
                    echo "Pushing image to docker"
                    docker.withRegistry('https://registry.hub.docker.com',"${DOCKER_HUB_CREDENTIALS_ID}"){
                        dockerImage.push('latest')
                    // }

                }
            }
        }
    }
}
}
