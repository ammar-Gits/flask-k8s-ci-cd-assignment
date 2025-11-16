# flask-k8s-ci-cd-assignment
Assignment repository for Flask app CI/CD deployment on Kubernetes.
# Flask Kubernetes CI/CD Assignment

## Project Description
This project demonstrates a complete CI/CD pipeline for a Flask web application using **GitHub Actions**, **Jenkins**, **Docker**, and **Kubernetes**.  
It covers automated builds, testing, deployment, rolling updates, scaling, and load balancing.

---

## Features

- **Dockerized Flask Application:** A simple "Hello, World!" Flask app packaged in a Docker image.
- **Kubernetes Deployment:** Deployment manifest with multiple replicas for scaling.
- **Rolling Updates:** Updates pods gradually with `maxSurge` and `maxUnavailable` configuration.
- **Scaling:** Dynamically scale the application using Kubernetes.
- **Load Balancing:** NodePort service distributes traffic across available replicas.
- **Continuous Integration:** Automated testing and linting using GitHub Actions.
- **Continuous Delivery:** Jenkins pipeline automates build, deployment, and verification in Kubernetes.

---

## Prerequisites

- Docker installed locally
- Minikube installed and running
- Jenkins installed and configured with kubectl access to Minikube
- Git installed

---

## Running Locally with Docker

1. **Build the Docker image:**
```bash
docker build -t myapp:latest .
Run the Docker container:

bash
Copy code
docker run -p 5000:5000 myapp:latest
Access the application:
Open your browser and go to http://localhost:5000

Deploying to Kubernetes via Jenkins
Start Minikube cluster:

bash
Copy code
minikube start
Trigger the Jenkins pipeline linked to the main branch. Pipeline stages:

Build Docker Image: Builds the Flask app Docker image.

Deploy to Kubernetes: Applies Deployment and Service manifests using kubectl apply.

Verify Deployment: Checks rollout status, verifies pods and services.

Access the application via NodePort:

bash
Copy code
kubectl get svc my-app-service
Use Minikube IP and NodePort to access the app in the browser.

Kubernetes Features Explained
Rolling Updates:
Gradually update pods to avoid downtime:

yaml
Copy code
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1
    maxUnavailable: 1
Scaling:
Scale replicas to handle more traffic:

bash
Copy code
kubectl scale deployment flask-app --replicas=3
Load Balancing:
NodePort Service distributes incoming traffic across replicas:

yaml
Copy code
kind: Service
type: NodePort
Rollback:
Undo a deployment if something goes wrong:

bash
Copy code
kubectl rollout undo deployment flask-app
Repository Structure
bash
Copy code
flask-k8s-ci-cd-assignment/
├── app.py                   # Flask application
├── requirements.txt         # Python dependencies
├── Dockerfile               # Multi-stage Dockerfile
├── kubernetes/
│   ├── deployment.yaml      # Kubernetes Deployment manifest
│   └── service.yaml         # Kubernetes Service manifest
├── Jenkinsfile              # Declarative Jenkins pipeline
├── .github/
│   └── workflows/ci.yml     # GitHub Actions workflow
└── README.md                # Project documentation
Authors
Admin: Repository setup, PR reviews, merges, Jenkins configuration

Developer: CI/CD pipeline implementation, Kubernetes manifests, documentation

