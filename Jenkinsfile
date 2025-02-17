pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                    git branch: 'main', credentialsId: 'gitops', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps'
            }
        }

        stage('Build Stage') {
            steps {
                echo "Build process starts here..."
                // Add actual build commands here, like Maven, Gradle, or npm
            }
        }
    }
}
