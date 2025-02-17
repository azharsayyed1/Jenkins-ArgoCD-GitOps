pipeline {
    agent any
    tools {
        nodejs 'NodeJS' // Ensure NodeJS is configured in Jenkins
    }
    environment {
        DOCKER_HUB_REPO = 'azharsayyed1222/jenkins-argocd-gitops'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'gitops', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps'
            }
        }
        stage('NPM Install') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }
        stage('Trivy Scan for Image') {
    steps {
        sh '''
            IMAGE_NAME="azharsayyed1222/jenkins-argocd-gitops:latest"
            SEVERITIES="HIGH,CRITICAL"

            TRIVY_JSON=$(trivy image --format json --no-progress "${IMAGE_NAME}")

            FILTERED_VULNS=$(echo "${TRIVY_JSON}" | jq -r ".Results[].Vulnerabilities[] | select(.Severity | in(\"${SEVERITIES//,/}\"))")

            if (!"${FILTERED_VULNS}".isEmpty()) {
                echo "${FILTERED_VULNS}" | jq -r '@. | [.[] | {VulnerabilityID, Severity, PackageName, Title}] | [.[] | [ .VulnerabilityID, .Severity, .PackageName, .Title ]] | @tsv' > trivy-scan-report.txt
                echo "Trivy scan report (HIGH, CRITICAL): trivy-scan-report.txt"
                
                // Fail the Jenkins build if vulnerabilities are found (recommended)
                error("High/Critical vulnerabilities found. Check trivy-scan-report.txt")  // Or a more specific message

            } else {
                echo "No ${SEVERITIES} vulnerabilities found." > trivy-scan-report.txt
                echo "No High/Critical vulnerabilities found."
            }

        '''
    }
}
    }
}
