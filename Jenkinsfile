pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/GeddaSuryaTejaswani/jenkins-project.git'
        IMAGE_NAME = 'jenkins-docker-demo'
        EMAIL_RECIPIENT = 'geddasuryatejaswani@gmail.com'
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
                echo "Cleaning up old containers and running a new one..."
                script {
                    // 🧩 Windows fix: use for-loop instead of xargs
                    bat '''
                    for /f "tokens=*" %%i in ('docker ps -q --filter "ancestor=%IMAGE_NAME%"') do docker stop %%i
                    for /f "tokens=*" %%i in ('docker ps -aq --filter "ancestor=%IMAGE_NAME%"') do docker rm %%i
                    '''

                    // 🧩 Run the container on port 5000
                    bat "docker run -d -p 5000:8080 %IMAGE_NAME%"
                }
            }
        }

        stage('Test App') {
            steps {
                echo "Testing Flask app endpoint..."
                script {
                    bat 'curl -f http://localhost:5000 || exit /b 1'
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
                mimeType: 'text/html',
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
                mimeType: 'text/html',
                to: "${EMAIL_RECIPIENT}"
            )
        }
    }
}

