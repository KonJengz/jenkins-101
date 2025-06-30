pipeline {
    agent any
    
    tools {
        // แก้ไขจาก 'docker' เป็น 'dockerTool' ให้ถูกต้องตาม Syntax ของ Jenkins
        dockerTool 'docker-latest' 
    }
    
    stages {
        stage('Clone') {
            steps {
               git url: 'https://github.com/KonJengz/jenkins-101.git', credentialsId: 'github-konjengz-pat', branch: 'main'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // ตอนนี้สามารถเรียก docker ได้โดยตรงและถูกต้อง
                sh 'docker build -t my-web-cicd .'
            }
        }
        
        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f my-web || true
                    docker run -d --name my-web -p 8080:80 my-web-cicd
                '''
            }
        }
    }
}

// pipeline {
//     agent any
//     stages {
//         stage('Clone') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/KonJengz/jenkins-101.git'
//             }
//         }
//         stage('Build Docker Image') {
//             steps {
//     sh 'export PATH=/usr/local/bin/docker:$PATH && docker build -t my-web-cicd .'
//             }
//         }
//         stage('Run Container') {
//             steps {  sh "docker run -d --name my-web-app -p 8080:80 my-web-cicd"}
//         }
//         stage('Cleanup') {
//             steps {
//                 sh 'docker rm -f my-web-app || exit 0'
//             }
//         }
//     }
// }