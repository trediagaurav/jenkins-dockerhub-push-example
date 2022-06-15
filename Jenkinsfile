pipeline {
  agent { label 'nodejs' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('tredia-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        bat 'docker build -t tredia/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        bat 'echo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        bat 'docker push tredia/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}
