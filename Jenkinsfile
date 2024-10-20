pipeline {
    agent any

    environment {
        IMAGE_NAME = 'cloud1111/jenkins-flask-app-demo'
        IMAGE_TAG = "${IMAGE_NAME}:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Test') {
            steps {
                echo "Test Stage"
                sh "whoami"
            }
        }

        stage('Login to Docker Hub') {
            steps {
                // Using Jenkins credentials to securely login to Docker Hub
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
                echo 'Login to Docker Hub successful'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_TAG} .'
                echo "Docker image built successfully"
                sh "docker images"
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push ${IMAGE_TAG}'
                echo "Docker image pushed successfully"
            }
        }
    }
}
