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
                script {
                    docker.build("python-jenkins-app")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image("python-jenkins-app").run("-p 5000:5000")
                }
            }
        }
    }
}
