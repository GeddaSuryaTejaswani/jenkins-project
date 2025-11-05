pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/GeddaSuryaTejaswani/jenkins-project.git'
        IMAGE_NAME = 'jenkins-docker-demo'
        EMAIL_RECIPIENT = 'your-email@example.com'
    }

    stages {
        stage('Checkout from Git') {
            steps {
                echo "Cloning the Git repository..."
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker container..."
                script {
                    docker.image("${IMAGE_NAME}").run('-d -p 8080:8080')
                }
            }
        }

        stage('Test App') {
            steps {
                echo "Testing Flask app endpoint..."
                script {
                    sh 'curl -f http://localhost:8080 || exit 1'
                }
            }
        }
    }

    post {
        success {
            echo "Build successful. Sending success email..."
            emailext(
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h3>Build Successful!</h3>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p><a href="${env.BUILD_URL}">View build details</a></p>
                """,
                to: "${EMAIL_RECIPIENT}"
            )
        }
        failure {
            echo "Build failed. Sending failure email..."
            emailext(
                subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h3>Build Failed!</h3>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>Check logs: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                to: "${EMAIL_RECIPIENT}"
            )
        }
    }
}
