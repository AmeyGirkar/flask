pipeline {
    agent {
        docker {
            image 'silverlogic/python3.8'
            args '-u root' // Optional: Run as root for installing packages if needed
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'python -m venv .venv'
                sh '''
                    . .venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    . .venv/bin/activate
                    pytest --junit-xml test-reports/results.xml application_test.py
                '''
            }
            post {
                always {
                    junit 'test-reports/*.xml'
                }
            }
        }
    }
}
