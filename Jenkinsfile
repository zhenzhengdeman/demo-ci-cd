pipeline {
    agent any

    stages {

        stage('Install') {
            steps {
                sh 'pip install flask'
            }
        }

        stage('Run App') {
            steps {
                sh 'python app.py &'
            }
        }

    }
}
