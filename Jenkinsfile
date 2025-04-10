pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
		git branch:'master', credentialsId:'github_creds', 'https://github.com/abdulrahmanalaa123/jenkins_npm'
		sh '''
		   git clone https://gitlab.com/twn-devops-bootcamp/latest/08-jenkins/jenkins-exercises
		   cp ./jenkins-excercises/app .
		   npm install ./app
		'''
		withCredentials([usernamePassword(credentialsId:'docker_login',usernameVariable:'USER',passwordVariable:'PASS')]){
			sh '''
				echo $PASS | docker login -u $USER --password-stdin
				docker build . -t tomatosoup3/node_nana:latest
				docker push tomatosoup3/node_nana:latest
			'''
		}
		sh 'docker container start --rm -d -p 3000:3000 tomatosoup3/node_nana:latest'
            }
        }
        stage('Test') {
            steps {
		
            }
        }
        stage('Deploy') {
            steps {
                //
            }
        }
    }
}
