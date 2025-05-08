pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        AWS_ACCOUNT_ID = '168126498869'    // Replace with your AWS account ID
        ECR_REPO = 'static-website'
        IMAGE_TAG = 'latest'
        ECR_URL = "168126498869.dkr.ecr.eu-north-1.amazonaws.com/static-web"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vikrantyadav1996/statics-web.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${ECR_URL}:${IMAGE_TAG} ."
            }
        }

        stage('Login to ECR') {
            steps {
                sh "aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
            }
        }

        stage('Push to ECR') {
            steps {
                sh "docker push ${ECR_URL}:${IMAGE_TAG}"
            }
        }
    }
}
