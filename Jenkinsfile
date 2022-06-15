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
        bat './jenkins/build.sh'
      }
    }
    stage('Login') {
      steps {
        bat './jenkins/login.sh'
      }
    }
    stage('Push') {
      steps {
        bat './jenkins/push.sh'
      }
    }
  }
  post {
    always {
      bat './jenkins/logout.sh'
    }
  }
}
