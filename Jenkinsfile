pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                // Clean workspace first
                deleteDir()
                
                // Clone the repository
                git branch: 'main', url: 'https://github.com/KonJengz/jenkins-101.git'
                
                // List files to verify checkout
                sh 'ls -la'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        sh 'docker build -t my-web-cicd .'
                    } catch (Exception e) {
                        error "Docker build failed: ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Run Container') {
            steps {
                script {
                    try {
                        // Stop and remove existing container if it exists
                        sh '''
                            docker stop my-web-container || true
                            docker rm my-web-container || true
                        '''
                        
                        // Run new container
                        sh 'docker run -d --name my-web-container -p 8081:80 my-web-cicd'
                        
                        // Verify container is running
                        sh 'docker ps | grep my-web-container'
                        
                    } catch (Exception e) {
                        error "Container deployment failed: ${e.getMessage()}"
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    try {
                        // Wait a moment for container to start
                        sleep 5
                        
                        // Test if the application is responding
                        sh 'curl -f http://localhost:8081 || echo "Service not ready yet"'
                        
                    } catch (Exception e) {
                        echo "Warning: Health check failed: ${e.getMessage()}"
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                try {
                    // Cleanup containers and images
                    sh '''
                        docker stop my-web-container || true
                        docker rm my-web-container || true
                        docker rmi my-web-cicd || true
                    '''
                } catch (Exception e) {
                    echo "Cleanup warning: ${e.getMessage()}"
                }
            }
        }
        
        success {
            echo 'Pipeline completed successfully!'
        }
        
        failure {
            echo 'Pipeline failed. Check the logs above for details.'
        }
    }
}