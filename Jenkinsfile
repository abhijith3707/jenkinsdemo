pipeline {
    agent {
        label 'Node1'
    }
    environment {
        IMAGE_NAME = 'cloud1111/jenkins-flask-app-demo'
        IMAGE_TAG = "${IMAGE_NAME}:${env.BUILD_NUMBER}"
        // KUBECONFIG = credentials('kubeconfig-credentials-id')
    }
    stages {
        stage('Test') {
            steps {
                // sh "pytest"
                echo "test"
                sh "whoami"
            }
        }
        stage('Login to docker hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                sh 'sudo docker login -u ${USERNAME} -p ${PASSWORD}'}
                echo 'Login successfully'
            }
        }
        stage('Build Docker Image')
        {
            steps
            {
                sh 'sudo docker build -t ${IMAGE_TAG} .'
                echo "Docker image build successfully"
                sh "sudo docker images"
            }
        }
        stage('Push Docker Image')
        {
            steps
            {
                sh 'sudo docker push ${IMAGE_TAG}'
                echo "Docker image push successfully"
            }
        }
        // stage('Deploy to EKS Cluster') {
        //     steps {
        //         sh "kubectl apply -f deployment.yaml"
        //         echo "Deployed to EKS Cluster"
        //     }
        // }
    }
}
