pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/KonJengz/jenkins-101.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-web-cicd .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker rm -f my-web || true'
                sh 'docker run -d --name my-web -p 8080:80 my-web-cicd'
            }
        }
    }
}


// pipeline {
//      agent {
//         docker {
//             image 'docker:latest'
//             args '-v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }
//     stages {
//         stage('Clone') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/KonJengz/jenkins-101.git', credentialsId: 'github-konjengz-pat'
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
       
//     }
// }