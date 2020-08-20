pipeline {
  agent any
  stages {
    stage('test aws') {
      steps {
        withAWS(region: 'us-east-1', credentials: 'aws_credentials') {
          sh '''
						aws sts get-caller-identity
					'''
        }

      }
    }

  }
}