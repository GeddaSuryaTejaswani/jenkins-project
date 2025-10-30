pipeline {
    agent any

    stages {
        stage('Checkout from Git') {
            steps {
                git 'https://github.com/GeddaSuryaTejaswani/jenkins-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    sh 'docker build -t my-jenkins-app .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    echo "Running Docker container..."
                    sh 'docker run -d --name myapp my-jenkins-app'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build completed successfully!"
        }
        failure {
            echo "❌ Build failed. Check logs."
        }
    }
}
