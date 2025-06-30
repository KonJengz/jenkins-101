pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/KonJengz/jenkins-101.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-web-cicd .'
            }
        }
        
        stage('Run Container') {
            steps {
                sh '''
                    docker stop my-web-container || true
                    docker rm my-web-container || true
                    docker run -d --name my-web-container -p 8081:80 my-web-cicd
                '''
            }
        }
        
        stage('Cleanup') {
            steps {
                sh '''
                    docker stop my-web-container || true
                    docker rm my-web-container || true
                    docker rmi my-web-cicd || true
                '''
            }
        }
    }
}