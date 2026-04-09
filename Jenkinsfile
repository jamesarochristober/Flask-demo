pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/jamesarochristober/Flask-demo.git'
            }
        }

        stage('Setup') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run') {
            steps {
                sh '''
                . venv/bin/activate
                pkill -f app.py || true
                nohup python app.py > app.log 2>&1 &
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'curl http://localhost:5000'
            }
        }
    }
}
