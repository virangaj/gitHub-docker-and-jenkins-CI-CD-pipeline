pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/virangaj/gitHub-docker-and-jenkins-CI-CD-pipeline'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t viranga97/node-app:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerbuh_pass', variable: 'dockerhub_pass')]) {
                    script {
                        bat "docker login -u viranga97 -p %dockerhub_pass%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push viranga97/node-app:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
