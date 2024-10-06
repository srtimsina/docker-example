pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = "suryaraj/mymobileapp"
        DOCKER_CREDENTIALS_ID = "dockerhub-cred"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/srtimsina/docker-example.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKER_HUB_REPO}:${BUILD_NUMBER} .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_HUB_CREDENTIALS}", passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh 'echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                    sh 'docker push ${DOCKER_HUB_REPO}:${BUILD_NUMBER}'
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
