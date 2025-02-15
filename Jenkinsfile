pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git(
                    branch: 'main', 
                    credentialsId: 'githubID', 
                    url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps.git'
                )
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
