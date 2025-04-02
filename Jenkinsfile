pipeline {
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
}
