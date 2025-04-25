pipeline {
    agent any

    environment {
        IMAGE_NAME = 'ecommerce-site'
        CONTAINER_NAME = 'ecommerce-container'
        HOST_PORT = '8081'
        CONTAINER_PORT = '80'
    }

    stages {
        stage('Clone Code') {
            steps {
                // Clone the repository from GitHub and specify the branch (main instead of master)
                git branch: 'main', url: 'https://github.com/saurav4578/devops.git' // Replace with your repo
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}", "./site")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop and remove existing container if running
                    sh "docker rm -f ${CONTAINER_NAME} || true"

                    // Run the container with new image
                    sh "docker run -d --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} ${IMAGE_NAME}"
                }
            }
        }
    }
}
