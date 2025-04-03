pipeline {
  agent any

  environment {
    DOCKER_HUB_USERNAME = 'kaveesha20'  // change this
    DOCKER_CREDENTIALS = credentials('341f52a6-9185-4440-82bb-f1172fdaca44')
    //DOCKER_CREDENTIALS_ID= 'docker-hub-credentials'
  }

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git' // change this
      }
    }

    stage('Build Docker Images') {
      steps {
        sh 'docker build -t $kaveesha20/backend ./backend'
        sh 'docker build -t $kaveesha20/frontend ./frontend'
      }
    }

    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('', DOCKER_CREDENTIALS) {
            sh 'docker push $kaveesha20/backend'
            sh 'docker push $kaveesha20/frontend'
          }
        }
      }
    }

    stage('Deploy via Docker Compose') {
      steps {
        sh 'docker-compose -f docker-compose.yml up -d --build'
      }
    }
  }
}