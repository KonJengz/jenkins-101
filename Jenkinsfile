// pipeline {
//     agent any
    
//      tools {
//         dockerTool 'docker-latest' // <-- แก้ไขเป็น dockerTool
//     }
    
//     stages {
//         stage('Clone') {
//             steps {
//                git url: 'https://github.com/KonJengz/jenkins-101.git', branch: 'main'
//             }
//         }
        
//         stage('Build Docker Image') {
//             steps {
//                 // ตอนนี้สามารถเรียก docker ได้โดยตรงและถูกต้อง
//                 sh 'docker build -t my-web-cicd .'
//             }
//         }
        
//         stage('Run Container') {
//             steps {
//                 sh '''
//                     docker rm -f my-web || true
//                     docker run -d --name my-web -p 8080:80 my-web-cicd
//                 '''
//             }
//         }
//     }
// }

// pipeline {
//     agent any
//     stages {
//         stage('Clone') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/sirawitWong/test1.git'
//             }
//         }
//         stage('Build Docker Image') {
//             steps {
//     sh 'export PATH=/opt/homebrew/bin:/usr/local/bin:$PATH && docker build -t my-web-cicd .'
//             }
//         }
//         stage('Run Container') {
//             steps { sh '''
//   export PATH=/opt/homebrew/bin:/usr/local/bin:$PATH
//                 docker rm -f my-web || true
//                 docker run -d --name my-web -p 9090:80 my-web-cicd
//          '''
//             }
//         }
//     }
// }

pipeline {
    agent any
    environment {
        // กำหนด PATH ให้กับทุก stage ใน Pipeline
        // โดยให้ /usr/local/bin (ที่อยู่ของ docker) มาก่อน PATH เดิม
        PATH = "/usr/local/bin:${env.PATH}"
    }
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/sirawitWong/test1.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                // ไม่จำเป็นต้อง export PATH อีกต่อไป
                sh 'docker build -t my-web-cicd .'
            }
        }
        stage('Run Container') {
            steps {
                // ไม่จำเป็นต้อง export PATH อีกต่อไป
                sh '''
                    docker rm -f my-web || true
                    docker run -d --name my-web -p 9090:80 my-web-cicd
                '''
            }
        }
    }
}