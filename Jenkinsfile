// pipeline {
//   agent any

//   environment {
//     DOCKER_HUB_USERNAME = 'kaveesha20'  // change this
//     DOCKER_CREDENTIALS = credentials('kaveesha20/****** (credintials for jenkins pipeline)')
//     //DOCKER_CREDENTIALS_ID= 'docker-hub-credentials'
//   }

//   stages {
//     stage('Clone Repo') {
//       steps {
//         git 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git' // change this
//       }
//     }

//     stage('Build Docker Images') {
//       steps {
//         sh 'docker build -t $kaveesha20/backend ./backend'
//         sh 'docker build -t $kaveesha20/frontend ./frontend'
//       }
//     }

//     stage('Push to Docker Hub') {
//       steps {
//         script {
//           docker.withRegistry('', DOCKER_CREDENTIALS) {
//             sh 'docker push $kaveesha20/backend'
//             sh 'docker push $kaveesha20/frontend'
//           }
//         }
//       }
//     }

//     stage('Deploy via Docker Compose') {
//       steps {
//         sh 'docker-compose -f docker-compose.yml up -d --build'
//       }
//     }
//   }
// }
pipeline {
  agent any

  environment {
    DOCKER_HUB_USERNAME = 'kaveesha20'
    DOCKER_CREDENTIALS = credentials('docker-hub-credentials') // Change this to your Jenkins credentials ID
  }

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git'
      }
    }

    stage('Build Docker Images') {
      steps {
        sh "docker build -t $DOCKER_HUB_USERNAME/backend ./backend"
        sh "docker build -t $DOCKER_HUB_USERNAME/frontend ./frontend"
      }
    }

    stage('Push to Docker Hub') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
            sh "docker push $kaveesha20/backend"
            sh "docker push $kaveesha20/frontend"
          }
        }
      }
    }

    stage('Deploy via Docker Compose') {
      steps {
        sh 'docker-compose -f docker-compose.yml up -d'
      }
    }
  }
}
