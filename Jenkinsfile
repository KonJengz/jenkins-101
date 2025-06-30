pipeline {
    agent any
    stages {
        // Stage 1: Clean workspace and check out source code
        stage('Checkout') {
            steps {
                // Good practice: always start with a clean workspace
                cleanWs()

                // This is the only checkout step you need.
                // It checks out the main branch from your repository.
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/KonJengz/jenkins-101.git']]
                ])
            }
        }

        // Stage 2: Build the Docker image from the Dockerfile
        stage('Build Docker Image') {
            steps {
                // This assumes a 'Dockerfile' is in your repository root
                sh 'docker build -t my-web-cicd .'
            }
        }

        // Stage 3: Stop any old container and run the new one
        stage('Run Container') {
            steps {
                // This command removes the old container if it exists.
                // '|| true' ensures the build doesn't fail if there's no container to remove.
                sh 'docker rm -f my-web || true'

                // This command runs your newly built image as a container.
                sh 'docker run -d --name my-web -p 8080:80 my-web-cicd'
            }
        }
    }
}