pipeline {
	agent any
	stages {
		
		

		stage('test aws') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws_credentials') {
					sh '''
						aws sts get-caller-identity
					'''
				}
			}
		}

		stage('Build Docker Image') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]){
					sh '''
						docker build -t andresaaap/cloudcapstonev2 .
					'''
				}
			}
		}



	}
}