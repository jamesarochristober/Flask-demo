node {

    stage('Checkout') {
        echo "Cloning repo..."
        git 'https://github.com/jamesarochristober/Flask-demo.git'
    }

    stage('Setup') {
        echo "Setting up Python..."
        sh '''
        python3 -m venv venv
        . venv/bin/activate
        pip install -r requirements.txt
        '''
    }

    stage('Run') {
        echo "Starting Flask..."
        sh '''
        . venv/bin/activate
        pkill -f app.py || true
        nohup python app.py > app.log 2>&1 &
        '''
    }

    stage('Test') {
        echo "Testing..."
        sh '''
        sleep 5
        curl http://localhost:5000
        '''
    }
}
