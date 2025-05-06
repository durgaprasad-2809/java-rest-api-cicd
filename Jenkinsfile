pipeline {
    agent any

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
    }

    post {
        success {
            echo "✅ Build successful!"
        }
        failure {
            echo "❌ Build failed."
        }
    }
}
