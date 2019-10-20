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
    stage('Building image') 
      {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
           }
      }
    stage('Deploying Image to DockerHub') {
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
