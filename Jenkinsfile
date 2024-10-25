pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/my-app' // Replace with your Docker Hub username and desired image name
        DOCKER_CREDENTIALS = 'dockerhub-credentials' // Name of the Jenkins Docker Hub credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git 'https://github.com/your-username/my-app.git' // Replace with your GitHub repo URL
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Log in to Docker Hub
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
                        sh 'docker push $DOCKER_IMAGE'
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
            echo 'Something went wrong. Check the logs.'
        }
    }
}
 
