pipeline {
  environment {
    registry = "an5028044/deploying"
    registryCredential = 'dockerhub1'
    dockerImage = ''
    dockerRun = ''
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
    
    stage('Deploy to Dev') {
      steps{
        dockerRun = docker run -d -p 9000:80 --name my-tomcat-app registry + ":$BUILD_NUMBER"
        sshagent(['54.175.12.190']) {
        sh "ssh -o StrictHostKeyChecking=no ec2-user@54.175.12.190 ${dockerRun}"
                                  }
           }                }
  }
}
