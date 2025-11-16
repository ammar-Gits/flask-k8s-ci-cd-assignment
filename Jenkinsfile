pipeline {
    agent any

    environment {
        // Set your kubeconfig path (Windows requires double backslashes)
        KUBECONFIG = "C:\\Users\\Kashan Ali\\.kube\\config"
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
                echo 'Applying Kubernetes manifests...'
                bat "kubectl apply -f kubernetes\\deployment.yaml"
                bat "kubectl apply -f kubernetes\\service.yaml"
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Checking rollout status...'
                bat "kubectl rollout status deployment/myapp-deployment"
                echo 'Listing pods and services...'
                bat "kubectl get pods"
                bat "kubectl get svc"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
