
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
            steps { sh '''

                docker rm -f my-web || true
                docker run -d --name my-web -p 9090:80 my-web-cicd
         '''
            }
        }
    }
}