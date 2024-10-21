pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'abhijithssss/jenkins-flask-app-demo'
        IMAGE_TAG = "${IMAGE_NAME}:${BUILD_NUMBER}"
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
                withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                }
                echo 'Login successfully'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_TAG} .'
                echo "Docker image built successfully"
                sh 'docker images'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                sh 'docker push ${IMAGE_TAG}'
                echo "Docker image pushed successfully"
            }
        }
    }

    post {
        success {
            mail to: 'abhijithsaseendran753@gmail.com',
                 subject: "SUCCESS: Jenkins Build #${BUILD_ID}",
                 body: "The Jenkins build ${BUILD_ID} for the Flask app was successful!"
        }
        failure {
            mail to: 'abhijithsaseendran753@gmail.com',
                 subject: "FAILURE: Jenkins Build #${BUILD_ID}",
                 body: "The Jenkins build ${BUILD_ID} for the Flask app failed. Please check the logs."
        }
    }
}
