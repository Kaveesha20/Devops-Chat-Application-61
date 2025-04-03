// // // pipeline {
// // //   agent any

// // //   environment {
// // //     DOCKER_HUB_USERNAME = 'kaveesha20'  // change this
// // //     DOCKER_CREDENTIALS = credentials('kaveesha20/****** (credintials for jenkins pipeline)')
// // //     //DOCKER_CREDENTIALS_ID= 'docker-hub-credentials'
// // //   }

// // //   stages {
// // //     stage('Clone Repo') {
// // //       steps {
// // //         git 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git' // change this
// // //       }
// // //     }

// // //     stage('Build Docker Images') {
// // //       steps {
// // //         sh 'docker build -t $kaveesha20/backend ./backend'
// // //         sh 'docker build -t $kaveesha20/frontend ./frontend'
// // //       }
// // //     }

// // //     stage('Push to Docker Hub') {
// // //       steps {
// // //         script {
// // //           docker.withRegistry('', DOCKER_CREDENTIALS) {
// // //             sh 'docker push $kaveesha20/backend'
// // //             sh 'docker push $kaveesha20/frontend'
// // //           }
// // //         }
// // //       }
// // //     }

// // //     stage('Deploy via Docker Compose') {
// // //       steps {
// // //         sh 'docker-compose -f docker-compose.yml up -d --build'
// // //       }
// // //     }
// // //   }
// // // }
// // pipeline {
// //   agent any

// //   environment {
// //     DOCKER_HUB_USERNAME = 'kaveesha20'
// //     DOCKER_CREDENTIALS = credentials('docker-hub-credentials') // Change this to your Jenkins credentials ID
// //   }

// //   stages {
// //     stage('Clone Repo') {
// //       steps {
// //         git 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git'
// //       }
// //     }

// //     stage('Build Docker Images') {
// //       steps {
// //         sh "docker build -t $DOCKER_HUB_USERNAME/backend ./backend"
// //         sh "docker build -t $DOCKER_HUB_USERNAME/frontend ./frontend"
// //       }
// //     }

// //     stage('Push to Docker Hub') {
// //       steps {
// //         script {
// //           docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
// //             sh "docker push $kaveesha20/backend"
// //             sh "docker push $kaveesha20/frontend"
// //           }
// //         }
// //       }
// //     }

// //     stage('Deploy via Docker Compose') {
// //       steps {
// //         sh 'docker-compose -f docker-compose.yml up -d'
// //       }
// //     }
// //   }
// // }
// pipeline {
//   agent any

//   environment {
//     DOCKER_HUB_USERNAME = 'kaveesha20'
//     DOCKER_CREDENTIALS = credentials('docker-hub-credentials') // Make sure this matches your Jenkins Credentials ID
//     FRONTEND_IMAGE = "${DOCKER_HUB_USERNAME}/frontend"
//     BACKEND_IMAGE = "${DOCKER_HUB_USERNAME}/backend"
//   }

//   stages {
//     stage('Clone Repository') {
//       steps {
//         git branch: 'develop', url: 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git'
//       }
//     }

//     stage('Build Docker Images') {
//       steps {
//         script {
//           sh "docker build -t ${FRONTEND_IMAGE} ./frontend"
//           sh "docker build -t ${BACKEND_IMAGE} ./backend"
//         }
//       }
//     }

//     stage('Push Docker Images to Docker Hub') {
//       steps {
//         script {
//           docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
//             sh "docker push ${FRONTEND_IMAGE}"
//             sh "docker push ${BACKEND_IMAGE}"
//           }
//         }
//       }
//     }

//     stage('Deploy using Docker Compose') {
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
    DOCKER_CREDENTIALS = credentials('docker-hub-credentials') // Your Jenkins credential ID
  }

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git'
      }
    }

    stage('Build Docker Images') {
      steps {
        bat "docker build -t %DOCKER_HUB_USERNAME%/backend ./backend"
        bat "docker build -t %DOCKER_HUB_USERNAME%/frontend ./frontend"
      }
    }

    stage('Push Docker Images to Docker Hub') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
            bat "docker push %DOCKER_HUB_USERNAME%/backend"
            bat "docker push %DOCKER_HUB_USERNAME%/frontend"
          }
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
