pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'prasad495/java-rest-api-cicd'
    }

    tools {
        maven 'Maven 3.8.6'  // Use the Maven version installed in Jenkins
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/durgaprasad-2809/java-rest-api-cicd.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
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
