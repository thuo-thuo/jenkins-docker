pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t thuo-thuo/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS | docker login -u $DOCKERHUB_CREDENTIALS --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push thuo-thuo/jenkins-docker-hub'
      }
    }
  }
  
  post {
    always {
      sh 'docker logout'
    }
  }
}