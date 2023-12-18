pipeline {
  agent any

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    IMAGE_NAME = 'lionnelpat/jenkins-hub'
  }

  stages {
    stage('Build') {
      steps {
        script {
          // Build Docker image
          docker.build(IMAGE_NAME)
        }
      }
    }

    stage('Push') {
      steps {
        script {
          // Docker login
          docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
            // Push Docker image to Docker Hub
            docker.image(IMAGE_NAME).push()
          }
        }
      }
    }
  }

  post {
    always {
      // Logout from Docker registry
      script {
        docker.image(IMAGE_NAME).withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
          docker.image(IMAGE_NAME).push()
        }
      }
    }
  }
}
