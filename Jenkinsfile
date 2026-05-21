pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t aws-devops-cicd-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop aws-devops-cicd-app || true'
                sh 'docker rm aws-devops-cicd-app || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name aws-devops-cicd-app -p 5000:5000 aws-devops-cicd-app'
            }
        }

        stage('Health Check') {
            steps {
                sh 'curl -f http://localhost:5000/health'
            }
        }
    }
}