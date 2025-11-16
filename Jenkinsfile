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
                echo 'Building Docker image inside Minikube...'
                // Use Minikube Docker daemon
                bat '''
                FOR /F "tokens=2 delims==" %%i IN ('minikube docker-env --shell cmd ^| find "DOCKER_HOST"') DO SET DOCKER_HOST=%%i
                FOR /F "tokens=2 delims==" %%i IN ('minikube docker-env --shell cmd ^| find "DOCKER_TLS_VERIFY"') DO SET DOCKER_TLS_VERIFY=%%i
                FOR /F "tokens=2 delims==" %%i IN ('minikube docker-env --shell cmd ^| find "DOCKER_CERT_PATH"') DO SET DOCKER_CERT_PATH=%%i
                docker build -t flask-app:latest .
                '''
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
