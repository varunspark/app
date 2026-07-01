pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = 'varunspark/app'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("app")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image("app").run("-p 5000:5000")
                }
            }
        }
    }
}
