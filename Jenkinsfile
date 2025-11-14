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
                    bat """
                    for /f "tokens=*" %%i in ('docker ps -q --filter "ancestor=${IMAGE_NAME}"') do docker stop %%i
                    for /f "tokens=*" %%i in ('docker ps -aq --filter "ancestor=${IMAGE_NAME}"') do docker rm %%i
                    docker run -d -p 5050:8080 --name jenkins_docker_demo ${IMAGE_NAME}
                    """
                }
            }
        }

        stage('Test App') {
            steps {
                echo "Testing Flask app endpoint..."
                script {
                    bat 'curl -f http://localhost:5050 || exit 1'
                }
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build Successful!",
                to: "${EMAIL_RECIPIENT}",
                from: "geddasuryatejaswani@gmail.com"
            )
        }
        failure {
            emailext(
                subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build Failed!",
                to: "${EMAIL_RECIPIENT}",
                from: "geddasuryatejaswani@gmail.com"
            )
        }
    }
}

