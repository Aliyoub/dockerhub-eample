pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('aliyoubinate-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t abi-alpine .'
      }
    }
  stage('tag image') {
      steps {
        sh 'docker tag abi-alpine alinbinapi/abi-alpine'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push alibinapi/abi-alpine'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
