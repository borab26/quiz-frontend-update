pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker_connect')

	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t bora2612b/frontendbyjenkins:v02 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push bora2612b/frontendbyjenkins:v02'
			}
		}

		stage ('Kubernetis deploy'){
			steps {
					sh ("/usr/local/bin/kubectl  apply -f frontend.yaml")
				
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

