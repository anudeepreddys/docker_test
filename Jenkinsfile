pipeline {
    environment { 
        registry = "anudeepreddys/docker_build" 
        registryCredential = 'docker-hub-credentials' 
        app = '' 
    }
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("docker_build")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
		stage('Push image') {
			steps {
		withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
			def registry_url = "registry.hub.docker.com/"
			bat "docker login -u $USER -p $PASSWORD ${registry_url}"
			docker.withRegistry("http://${registry_url}", "docker-hub-credentials") {
				// Push your image now
				bat "docker push anudeepreddys/docker_build:build"
			}
		}
		}
	}
  }
}
