pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out successfully'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    venv/bin/pip install -r app/requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'venv/bin/python -m pytest -v'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t jenkins-flask-app:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f jenkins-flask-container || true
                    docker run -d \
                        --name jenkins-flask-container \
                        -p 5000:5000 \
                        jenkins-flask-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    sleep 5
                    curl -f http://host.docker.internal:5000/health
                '''
            }
        }
    }
}