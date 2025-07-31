pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/chamithgithub/ci-cd-pipeline'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t chamithrs/wonderful:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhubpass', variable: 'dockerhubpass')]) {
    // some block
                 bat "docker login -u chamithrs -p %dockerhubpass%"
                    }  
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push chamithrs/wonderful:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
