
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t flask-ci-cd-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm flask-ci-cd-app python -m pytest -v'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker rm -f flask-ci-cd-container || true
                    docker run -d --name flask-ci-cd-container -p 5000:5000 flask-ci-cd-app
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps --filter name=flask-ci-cd-container'
            }
        }
    }
}
