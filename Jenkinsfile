pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t flask-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests... (none for now)'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment step placeholder.'
            }
        }
    }
}
