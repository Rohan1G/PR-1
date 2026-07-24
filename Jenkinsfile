pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                sh 'node --version'
                sh 'npm --version'
                sh 'docker --version'
                sh 'docker compose version'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t node-todo-app .'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                docker compose down || true
                docker compose up -d --build
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
