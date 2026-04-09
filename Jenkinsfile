node {

    stage('Checkout') {
        echo "Cloning repo..."
        // Explicitly set the main branch
        git branch: 'main', url: 'https://github.com/jamesarochristober/Flask-demo.git'
    }

    stage('Setup') {
        echo "Setting up Python..."
        sh '''
        python3 -m venv venv
        # Use venv/bin/pip explicitly to avoid sourcing issues
        ./venv/bin/pip install --upgrade pip
        ./venv/bin/pip install -r requirements.txt
        '''
    }

    stage('Run') {
        echo "Starting Flask..."
        sh '''
        # Kill any previous app.py instances
        pkill -f app.py || true
        # Start Flask in background using venv Python
        nohup ./venv/bin/python app.py > app.log 2>&1 &
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
