pipeline {
    agent any
    
    stages {
        stage('Setup') {
            steps {
                echo 'Creating Python virtual environment...'
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install pytest
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                echo 'Installing project dependencies...'
                sh '''
                    . venv/bin/activate
                    if [ -f requirements.txt ]; then
                        pip install -r requirements.txt
                    fi
                '''
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Running unit tests from test_main.py...'
                sh '''
                    . venv/bin/activate
                    pytest test_main.py -v
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up virtual environment...'
            sh 'rm -rf venv'
        }
        success {
            echo 'All tests passed successfully!'
        }
        failure {
            echo 'Tests failed! Check the logs above.'
        }
    }
}
