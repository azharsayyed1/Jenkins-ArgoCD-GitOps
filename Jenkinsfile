pipeline {
	agent any

	environment {

	}
	stages {
		stage('Checkout Github'){
			steps {
				git branch: 'main', credentialsId: '1b892a0e-0126-49a4-bf4a-bcc1d822daaf', url: 'https://github.com/azharsayyed1/Jenkins-ArgoCD-GitOps.git'	
			}
		}		
