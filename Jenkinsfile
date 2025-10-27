pipeline {
    agent any

    environment {
        // Update this after you share your DockerHub image name
        IMAGE_NAME = "YOUR_DOCKERHUB_USERNAME/YOUR_REPO_NAME"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Pulling code from Git repo..."
                git branch: 'main', url: 'https://github.com/jubairthematics/harshcicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    dockerImage = docker.build("${env.IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo "📌 TODO: Add Trivy or Snyk scanning stage here"
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    echo "Logging into DockerHub..."
                    docker.withRegistry('', 'dockerhub-credentials') {
                        // No-op, just login
                    }
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    echo "Pushing Docker image to DockerHub..."
                    docker.withRegistry('', 'dockerhub-credentials') {
                        dockerImage.push("${env.BUILD_NUMBER}")
                        dockerImage.push("latest")
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "📌 TODO: Add kubectl apply -f deployment.yaml once K8s is configured"
            }
        }
    }
}
