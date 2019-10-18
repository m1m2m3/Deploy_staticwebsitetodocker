pipeline {
  environment {
    registry = "an5028044/dockerpipeline"
    registryCredential = 'dockerhub1'
    dockerImage = ''
  }
  agent any
  stages {
    stage('SCM checkout') {
      steps {
        git 'https://github.com/m1m2m3/CI-CD-with-Docker.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploying Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    
  }
}
