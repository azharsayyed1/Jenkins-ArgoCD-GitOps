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
        stage('Install Kubectl & ArgoCD CLI') {
    steps {
        sh '''
        echo 'Installing Kubectl & ArgoCD CLI...'

        # Install Kubectl
        curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
        chmod +x kubectl
        sudo mv kubectl /usr/local/bin/kubectl

        # Install ArgoCD CLI
        curl -sSL -o argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
        chmod +x argocd
        sudo mv argocd /usr/local/bin/argocd
        '''
    }
}


}
}
