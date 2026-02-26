pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                echo 'Building C++ backend Docker image...'
                dir('CC_LAB-6') {
                    sh 'docker build -t backend-app ./backend'
                }
            }
        }

        stage('Build NGINX') {
            steps {
                echo 'Pulling NGINX image...'
                sh 'docker pull nginx'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying containers...'
                sh 'docker stop backend-app-container || true'
                sh 'docker rm backend-app-container || true'
                sh 'docker run -d --name backend-app-container -p 8081:8081 backend-app'
            }
        }

        stage('Verify') {
            steps {
                echo 'Verifying deployment...'
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
