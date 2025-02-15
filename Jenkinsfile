pipeline {
	agent any

	environment {

	}
	stages {
		stage('Checkout Github'){
			steps {
					git branch: 'main', credentialsId: 'githubID', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps.git'
			}
		}		
	}
}