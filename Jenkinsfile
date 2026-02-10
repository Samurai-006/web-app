pipeline{
	agent any
	stages{
		stage('Build docker'){
			steps{
				sh 'docker build -t python-webapp .'
			}
		}
		stage('Deploy Container'){
			steps{
				sh 'docker run -d -p 5000:5000 --name python-webapp python-webapp'
			}
		}
	}
}
