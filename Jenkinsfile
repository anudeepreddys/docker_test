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
    stage('Deploy to DOcker') {
      steps {
        sh "docker login -u anudeepreddys -p dckr_pat_Rakxneo2JbqnrvkvfbVkCxvNwXk"
        sh "docker run -p 3000:3000 anudeepreddys/docker_build:$BUILD_NUMBER"
      }
    }
  }
}
