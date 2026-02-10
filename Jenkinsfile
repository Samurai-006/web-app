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
		        withCredentials([usernamePassword(
		            credentialsId: 'git-cred',
		            usernameVariable: 'GIT_USER',
		            passwordVariable: 'GIT_PASS'
		        )]) {
		            bat '''
		            git config user.email "jenkins@local"
		            git config user.name "Jenkins"
		
		            git checkout -B stable-builds
		            git push https://%GIT_USER%:%GIT_PASS%@github.com/Samurai-006/web-app.git stable-builds --force
		            '''
		        }
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
