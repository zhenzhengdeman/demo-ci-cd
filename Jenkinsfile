pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest tests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t demo-ci-cd:latest .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                docker stop demo-ci-cd || true
                docker rm demo-ci-cd || true
                docker run -d --name demo-ci-cd -p 5000:5000 demo-ci-cd:latest
                '''
            }
        }

    }
}
