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
        script {
          checkout scm
        }
      }
    }
    stage('Build') {
      steps {
        script {
          app = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Test') {
      steps {
        echo 'Empty'
      }
    }
    stage('Push image') {
      steps {
        script {
          docker.withRegistry("", registryCredential) {
            app.push()
          }
        }
      }
    }
  }
}
