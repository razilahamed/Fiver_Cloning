pipeline {
    agent any 

    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'master', url: 'https://github.com/razilahamed/Fiver_Cloning.git'
                }
            }
        }
        stage('Build Backend Docker Image') {
            steps {  
                dir('backend') {
                    bat 'docker build -t razilahamed/backend:%BUILD_NUMBER% .'
                }
            }
        }
        stage('Build Frontend Docker Image') {
            steps {
                dir('frontend') {
                    bat 'docker build -t razilahamed/frontend:%BUILD_NUMBER% .'
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-password', variable: 'dockerpass')]) {
                    script {
                        bat "docker login -u razilahamed -p %dockerpass%"
                    }
                }
            }
        }
        stage('Push Backend Image') {
            steps {
                bat 'docker push razilahamed/backend:%BUILD_NUMBER%'
            }
        }
        stage('Push Frontend Image') {
            steps {
                bat 'docker push razilahamed/frontend:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
