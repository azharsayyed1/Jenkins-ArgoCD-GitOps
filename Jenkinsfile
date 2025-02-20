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
# Download ArgoCD CLI
curl -sSL -o argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64

# Make it executable
chmod +x argocd

# Move to /usr/local/bin (requires sudo)
sudo mv argocd /usr/local/bin/argocd


        '''
    }
}

stage('Apply Kubernetes Manifests & Sync App with ArgoCD'){
			steps {
				script {
					kubeconfig(credentialsId: 'kubeconfig', serverUrl: 'https://192.168.49.2:8443') {
    						sh '''
						argocd login 54.196.125.205:30890 --username admin --password $(kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d) --insecure
						argocd app sync argocdjenkins
						'''
					}	
				}
			}
		}


}
}
