pipeline {
    agent any

    environment {
        IMAGE_NAME = "your-dockerhub-user/flask-app"
        TAG = "latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f kubernetes/deployment.yaml'
                sh 'kubectl apply -f kubernetes/service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'kubectl rollout status deployment/flask-deployment'
                sh 'kubectl get pods'
                sh 'kubectl get svc'
            }
        }
    }
}
