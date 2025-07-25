pipeline {
    agent any

    parameters {
        string(name: 'TARGET_IP', defaultValue: '127.0.0.1', description: 'Target IP for scanning')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Lint') {
            steps {
                sh '''
                    . venv/bin/activate
                    pip install flake8
                    flake8 main.py
                '''
            }
        }
        stage('Run Scan') {
            steps {
                sh '''
                    . venv/bin/activate
                    python main.py 127.0.0.1
                '''
            }
        }
    }
}