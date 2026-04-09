pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning repo..."
                git branch: 'main', url: 'https://github.com/jamesarochristober/Flask-demo.git'
            }
        }

        stage('Setup') {
            steps {
                echo "Setting up Python..."
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run') {
            steps {
                echo "Starting Flask app..."
                sh '''
                . venv/bin/activate
                pkill -f app.py || true
                nohup python app.py > app.log 2>&1 &
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Testing app..."
                sh '''
                sleep 5
                curl http://localhost:5000
                '''
            }
        }
    }
}
