pipeline {
    agent any

    environment {
        // Path to kubeconfig (use double backslashes for Windows)
        KUBECONFIG = "C:\\Users\\Kashan Mehdi\\.kube\\config"
        // Docker image name
        DOCKER_IMAGE = "myapp:latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat "docker build -t %DOCKER_IMAGE% ."
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying to Kubernetes...'
                // Apply Deployment and Service manifests
                bat "kubectl apply -f kubernetes\\deployment.yaml"
                bat "kubectl apply -f kubernetes\\service.yaml"
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Checking deployment rollout...'
                bat "kubectl rollout status deployment/flask-app"
                echo 'Listing all pods...'
                bat "kubectl get pods"
                echo 'Listing services...'
                bat "kubectl get svc"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check the console output for errors.'
        }
    }
}
