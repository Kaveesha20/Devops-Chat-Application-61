/*pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t myapp .'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh 'docker run myapp npm test'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: DOCKER_CREDENTIALS_ID]) {
                    sh 'docker tag myapp mydockerhubusername/myapp:latest'
                    sh 'docker push mydockerhubusername/myapp:latest'
                }
            }
        }
    }
}*/
/*pipeline {
  agent any

  environment {
    DOCKER_HUB_USERNAME = 'tharushi104'  // change this
    DOCKER_CREDENTIALS = credentials('dockerhub-creds')
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
        sh 'docker build -t $tharushi104/backend ./backend'
        sh 'docker build -t $tharushi104/frontend ./frontend'
      }
    }

    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('', DOCKER_CREDENTIALS) {
            sh 'docker push $tharushi104/backend'
            sh 'docker push $tharushi104/frontend'
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
}*/
pipeline {
  agent any

  environment {
    DOCKER_HUB_USERNAME = 'tharushi104'
    DOCKER_CREDENTIALS = credentials('dockerhub-creds')
  }

  stages {
    stage('Build Docker Images') {
      steps {
        sh 'docker build -t ${DOCKER_HUB_USERNAME}/backend ./backend'
        sh 'docker build -t ${DOCKER_HUB_USERNAME}/frontend ./frontend'
      }
    }

    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('', DOCKER_CREDENTIALS) {
            sh 'docker push ${DOCKER_HUB_USERNAME}/backend'
            sh 'docker push ${DOCKER_HUB_USERNAME}/frontend'
          }
        }
      }
    }

    stage('Deploy via Docker Compose') {
      steps {
        sh 'docker-compose down || true'
        sh 'docker-compose up -d --build'
      }
    }
  }
}
