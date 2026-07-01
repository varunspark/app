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

        stage('Docker Logout') {
            steps {
                sh 'docker logout || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    docker.image("${IMAGE_NAME}:${BUILD_NUMBER}").push()
                    docker.image("${IMAGE_NAME}:${BUILD_NUMBER}").push('latest')
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f app-container || true'
                script {
                    docker.image("${IMAGE_NAME}:${BUILD_NUMBER}").run("--name app-container -p 5000:5000")
                }
            }
        }
    }
}
