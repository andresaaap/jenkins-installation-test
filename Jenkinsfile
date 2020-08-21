pipeline {
  agent any
  stages {
    stage('test aws') {
      steps {
        withAWS(region: 'us-east-2', credentials: 'aws_credentials') {
          sh '''
						aws sts get-caller-identity
					'''				}
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

		stage('create kube config file') {
	      steps {
	        withAWS(region: 'us-east-2', credentials: 'aws_credentials') {
	          sh '''
							aws eks --region us-east-2 update-kubeconfig --name jenkinstest
						'''				}
				}
		}

		stage('deploy') {
	      steps {
	        withAWS(region: 'us-east-2', credentials: 'aws_credentials') {
	          sh '''
							kubectl apply -f ./blue-controller.json
							kubectl apply -f ./blue-service.json
						'''				}
				}
		}



  }
}