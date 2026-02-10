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
		stage('Unit Test'){
			steps{
				bat '''
				pip install -r requirements.txt
				pip install pytest
				python -m pytest
				echo "Test Successful"
				'''
			}
		}
		stage('Delivering'){
			steps{
				bat 'git push -u origin stable build'
			}
		}
	}
}
