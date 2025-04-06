pipeline {
  agent any

  environment {
    DOCKER_HUB_USERNAME = 'kaveesha20'
    DOCKER_CREDENTIALS = credentials('docker-hub-credentials')
  }

  stages {
    stage('Clone Repo') {
      steps {
        git branch: 'develop', url: 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git'
      }
    }

    stage('Build Docker Images') {
      steps {
        bat "docker build -t ${DOCKER_HUB_USERNAME}/backend ./backend"
        bat "docker build -t ${DOCKER_HUB_USERNAME}/frontend ./frontend"
      }
    }

    stage('Push Docker Images to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
          bat "docker push ${DOCKER_HUB_USERNAME}/backend"
          bat "docker push ${DOCKER_HUB_USERNAME}/frontend"
        }
      }
    }

    stage('Deploy using Docker Compose') {
      steps {
        bat 'docker-compose -f docker-compose.yml up -d --build'
      }
    }
  }
}
