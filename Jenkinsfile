pipeline {
    agent any

    environment {
        DOCKER_HUB_USERNAME = ''
        DOCKER_HUB_PASSWORD = ''
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository containing Dockerfiles and configuration
                checkout scm
            }
        }
        
        stage('Build Loki Image') {
            steps {
                script {
                    // Build the Loki Docker image from Dockerfile.loki
                    sh 'docker build -t $DOCKER_HUB_USERNAME/loki:latest -f Dockerfile.loki .'
                }
            }
        }

        stage('Build Promtail Image') {
            steps {
                script {
                    // Build the Promtail Docker image from Dockerfile.promtail
                    sh 'docker build -t $DOCKER_HUB_USERNAME/promtail:latest -f Dockerfile.promtail .'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub using provided credentials
                    sh 'echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin'
                }
            }
        }

        stage('Push Loki Image to Docker Hub') {
            steps {
                script {
                    // Push the Loki image to Docker Hub
                    sh 'docker push $DOCKER_HUB_USERNAME/loki:latest'
                }
            }
        }

        stage('Push Promtail Image to Docker Hub') {
            steps {
                script {
                    // Push the Promtail image to Docker Hub
                    sh 'docker push $DOCKER_HUB_USERNAME/promtail:latest'
                }
            }
        }

        stage('Deploy to Minikube') {
            steps {
                script {
                    // Apply the Kubernetes configuration files to Minikube
                    sh 'kubectl apply -f loki-config.yaml'
                    sh 'kubectl apply -f promtail-config.yaml'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline execution was successful!'
        }

        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
