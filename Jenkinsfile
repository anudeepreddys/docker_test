pipeline {
  environment {
    registry = "anudeepreddys/docker_build"
    registryCredential = 'docker_hub'
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
    stages('Deploy to Kubernetes') {
        steps {
            sh "kubectl apply -f sample_app.yaml"
        }
    }
  }
}
