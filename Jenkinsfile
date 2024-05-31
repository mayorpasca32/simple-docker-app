
pipeline {
    agent any

    environment {
        // Define environment variables for Docker Hub credentials
        DOCKER_HUB_USERNAME = credentials('mayorpasca32')
        DOCKER_HUB_PASSWORD = credentials('Popoola32.')
        DOCKER_IMAGE_NAME = 'mayorpasca32/deployment'
        DOCKER_IMAGE_TAG = 'latest'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                // Checkout source code from repository
                checkout scm

                // Build Docker image
                script {
                    dockerImage = docker.build("${mayorpasca32/deployment}:${latest}", "-f Dockerfile .")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${mayorpasca32}", "${Popoola32.}") {
                        // Push Docker image to Docker Hub
                        dockerImage.push("${latest}")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully!'
        }
        failure {
            echo 'Failed to build or push Docker image.'
        }
    }
}
