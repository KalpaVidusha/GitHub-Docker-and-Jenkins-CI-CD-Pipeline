pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/KalpaVidusha/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t vidusha01/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhub-pw')]) {
                    script {
                        bat "docker login -u vidusha01 -p %dockerhub-pw%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push vidusha01/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
