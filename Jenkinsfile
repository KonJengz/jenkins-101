// pipeline {
//     agent any
//     stages {
//         stage('Clone') {
//             steps {
//                git url: 'https://github.com/KonJengz/jenkins-101.git', credentialsId: 'github-konjengz-pat', branch: 'main'
//             }
//         }
//         stage('Build Docker Image') {
//             steps {
//                 sh 'docker build -t my-web-cicd .'
//             }
//         }
//         stage('Run Container') {
//             steps {
//                 sh 'docker rm -f my-web || exit 0'
//                 sh 'docker run -d --name my-web -p 8080:80 my-web-cicd'
//             }
//         }
//     }
// }

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
    sh 'export PATH=/opt/homebrew/bin:/usr/local/bin:$PATH && docker build -t my-web-cicd .'
            }
        }
        stage('Run Container') {
            steps {  sh "docker run -d --name my-web-app -p 8080:80 my-web-cicd"}
        }
        stage('Cleanup') {
            steps {
                sh 'docker rm -f my-web-app || exit 0'
            }
        }
    }
}