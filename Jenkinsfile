pipeline {
    agent any
    // tools {
    //     dockerTool 'docker'
    // }
    environment {
        IMAGE_NAME = 'abhijithssss/jenkins-flask-app-demo'
        IMAGE_TAG = "${IMAGE_NAME}:${env.BUILD_NUMBER}"
    }
    stages {
        stage('Test') {
            steps {
                echo "Test Stage"
                sh "whoami"
            }
        }
        stage('Login to docker hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                sh 'docker login -u ${USERNAME} -p ${PASSWORD}'}
                echo 'Login successfully'
            }
        }
        stage('Build Docker Image')
        {
            steps
            {
                sh 'docker build -t ${IMAGE_TAG} .'
                echo "Docker image build successfully"
                sh "docker images"
            }
        }
        
        // stage('Login to Docker Hub') {
        //     steps {
        //         // Using Jenkins credentials to securely login to Docker Hub
        //         withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
        //             sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
        //         }
        //     }
        // }
        stage('Push Docker Image')
        {
            steps
            {
                sh 'docker push ${IMAGE_TAG}'
                echo "Docker image push successfully"
            }
        }
    }
}
post {
        success {
            mail to: 'abhijithsaseendran753@gmail.com',
                 subject: "SUCCESS: Jenkins Build #${env.BUILD_ID}",
                 body: "The Jenkins build ${env.BUILD_ID} for the Node-React app was successful!"
        }
        failure {
            mail to: 'abhijithsaseendran753@gmail.com',
                 subject: "FAILURE: Jenkins Build #${env.BUILD_ID}",
                 body: "The Jenkins build ${env.BUILD_ID} for the Node-React app failed. Please check the logs."
        }
    }
}
