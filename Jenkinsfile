pipeline{
	agent any
	stages{
		stage('Installing dependencies'){
			steps{
				bat'''
				pip install -r requirements.txt
				pip install pytest
				'''
			}
		}
		stage('Unit Test'){
			steps{
				bat '''
				python -m pytest
				echo "Test Successful"
				'''
			}
		}
		stage('Delivering') {
		    steps {
				bat 'git ls-remote https://github.com/Samurai-006/web-app.git'
		        bat 'git checkout -B stable-builds'
				bat 'git push origin stable-builds --force --verbose'
			}
		}

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
