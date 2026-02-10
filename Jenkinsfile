pipeline{
	agent any
	stages{
		stage('Build docker'){
			steps{
				bat 'docker build -t python-webapp .'
			}
		}
		stage('Deploy Container'){
			steps{
				bat ''' 
				docker stop python-webapp
				docker rm python-webapp
				docker run -d -p 5000:5000 --name python-webapp python-webapp
				'''
			}
		}
	}
}
