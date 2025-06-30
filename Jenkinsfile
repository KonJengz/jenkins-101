pipeline {
    agent any
    
    tools {
        // ใช้ชื่อ Docker tool ที่คุณตั้งค่าไว้ใน Global Tool Configuration
        docker 'docker-latest' 
    }
    
    stages {
        stage('Clone') {
            steps {
               git url: 'https://github.com/KonJengz/jenkins-101.git', credentialsId: 'github-konjengz-pat', branch: 'main'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // ไม่ต้อง export PATH อีกต่อไป!
                sh 'docker build -t my-web-cicd .'
            }
        }
        
        stage('Run Container') {
            steps {
                // รวมคำสั่งไว้ใน sh block เดียวกันเพื่อความเรียบร้อย
                sh '''
                    docker rm -f my-web || true
                    docker run -d --name my-web -p 8080:80 my-web-cicd
                '''
                // หมายเหตุ: `|| true` ทำหน้าที่เหมือน `|| exit 0` คือไม่ให้ build fail ถ้า container ไม่มีอยู่
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