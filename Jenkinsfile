pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'prasad495/java-rest-api-cicd'  // Docker image name
    }

    tools {
        maven 'Maven 3.8.6'  // Make sure Maven is installed globally in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repo, make sure you're pointing to the correct branch
                git branch: 'main', url: 'https://github.com/durgaprasad-2809/java-rest-api-cicd.git'
            }
        }

        stage('Build with Maven') {
            steps {
                // Build the project using Maven
                sh 'mvn clean install'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    // Log in to Docker Hub
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    // Push the Docker image to Docker Hub
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build & push successful!"
        }
        failure {
            echo "❌ Build failed."
        }
    }
}
