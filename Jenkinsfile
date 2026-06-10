pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                // GitHub එකෙන් කේතය ලබා ගැනීම
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                // Docker Image එක හැදීම
                sh 'docker build -t demo-inventory:latest .'
            }
        }
        stage('Deploy Application') {
            steps {
                // පරණ ඒවා අයින් කරලා අලුත් Container එක run කිරීම
                sh '''
                    docker stop inventory-app || true
                    docker rm inventory-app || true
                    docker run -d -p 8081:80 --name inventory-app demo-inventory:latest
                '''
            }
        }
    }
}
