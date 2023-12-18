pipeline {
  environment {
    registry = "lionnelpat/jenkins-hub"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning our Git') {
      steps {
        git 'https://github.com/lionnelpat/jenkins-hub.git'
      }
    }
    stage('Building our image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    stage('Deploy our image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Cleaning up') {
      steps{
        sh "docker rmi $registry"
      }
    }
  }
}