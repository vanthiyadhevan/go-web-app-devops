pipeline {
	agent any 
	environment {
		DOCKER_USERNAME = credentials('docker_creds')
		DOCKER_PASSWORD = credentials('docker_creds')
		DOCKER_IMAGENAME = 'go-web-app-devops'
		DOCKER_REGISTRYNAME = 'vanthiyadevan'
	}
	stages {
		stage('CheckOut') {
			steps {
				git url: 'https://github.com/vanthiyadhevan/go-web-app-devops.git', branch: 'main' 
			}
		}
		stage('Build Docker image') {
			steps {
				script {
					docker_image = docker.build("${DOCKER_REGISTRYNAME}/${DOCKER_IMAGENAME}:${BUILD_NUMBER}", "." )
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script {
					withDockerRegistry(credentialsId: 'docker_creds', url: 'https://index.docker.io/v1/') {
						docker_image.push()
					}
				}
			}
		}
	}
}