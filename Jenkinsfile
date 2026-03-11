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
                sh '''
		python3 -m venv venv
		. venv/bin/activate
		pip install --upgrade pip
		pip3 install -r requirements.txt
		'''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
		. venv/bin/activate
		export PYTHONPATH=$PWD
		pytest tests
		'''
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Build step finished"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                pkill -f app.py || true
                nohup python3 app.py > app.log 2>&1 &
                '''
            }
        }

    }
}
