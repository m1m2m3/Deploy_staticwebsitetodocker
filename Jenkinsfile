pipeline {
  environment {
    registry = "an5028044/deploying"
    registryCredential = 'dockerhub1'
    dockerImage = ''
  }
  agent any
  stages {
    stage('SCM checkout') {
      steps {
        git 'https://github.com/m1m2m3/Deploy_staticwebsitetodocker.git'
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
    stage('Creating Container') {
      steps{
        sh 'docker run -it -d -p 9001:80 registry + ":$BUILD_NUMBER"'
      }
    }
    
  }
}
