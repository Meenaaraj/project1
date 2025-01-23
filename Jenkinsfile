pipeline {
    agent any
    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG = "2.0"
        REGISTRY = "meenaaraj"
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/your-repository/myapp.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t $REGISTRY/$IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                script {
                    // Run tests (if any, you can add test scripts here)
                    echo "Running tests..."
                    // You can add `pytest` or another testing framework if needed
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push the image to Docker registry
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push $REGISTRY/$IMAGE_NAME:$IMAGE_TAG'
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Apply the Kubernetes configurations (Deployment & Service)
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
        
        stage('Clean Up') {
            steps {
                // Clean up old Docker images and Kubernetes pods if needed
                sh 'docker system prune -f'
            }
        }
    }
    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}

