// pipeline {
//   agent any

//   environment {
//     DOCKER_HUB_USERNAME = 'kaveesha20'
//     DOCKER_CREDENTIALS = credentials('docker-hub-credentials')
//   }

//   stages {
//     stage('Clone Repo') {
//       steps {
//         git branch: 'develop', url: 'https://github.com/Kaveesha20/Devops-Chat-Application-61.git'
//       }
//     }

//     stage('Build Docker Images') {
//       steps {
//         bat "docker build -t ${DOCKER_HUB_USERNAME}/backend ./backend"
//         bat "docker build -t ${DOCKER_HUB_USERNAME}/frontend ./frontend"
//       }
//     }

//     stage('Push Docker Images to Docker Hub') {
//       steps {
//         withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
//           bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
//           bat "docker push ${DOCKER_HUB_USERNAME}/backend"
//           bat "docker push ${DOCKER_HUB_USERNAME}/frontend"
//         }
//       }
//     }

//     stage('Deploy using Docker Compose') {
//       steps {
//         bat 'docker-compose -f docker-compose.yml up -d --build'
//       }
//     }
//   }
// }
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
                    bat "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                    bat "docker push ${DOCKER_HUB_USERNAME}/backend"
                    bat "docker push ${DOCKER_HUB_USERNAME}/frontend"
                }
            }
        }

        stage('Deploy to AWS EC2') {
            steps {
                withCredentials([file(credentialsId: 'ec2-private-key', variable: 'PEM_KEY')]) {
                    // Copy docker-compose.yml to EC2 instance (escaped backslashes for Windows path)
                    bat "scp -i ${PEM_KEY} -o StrictHostKeyChecking=no \"C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\New CI,CD pipeline\\docker-compose.yml\" ec2-user@16.171.18.112:/home/ec2-user"

                    // SSH into EC2 and run docker-compose to deploy the app
                    bat "ssh -i ${PEM_KEY} -o StrictHostKeyChecking=no ec2-user@16.171.18.112 \"docker-compose -f /home/ec2-user/docker-compose.yml up -d --build\""
                }
            }
        }
    }
}
