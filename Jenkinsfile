pipeline {
    agent any


    stages {
        stage('Checkout Code') {
            steps {
                checkout scmGit(branches: [[name: 'email-notification']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/eayar123/trainmefordevsecops.git']])
            }
        }
        
        stage('SAST'){
            steps{
                sh ''
            }
        }
        
        stage('build'){
            steps{
                sh ''
            }
        }
        
        stage('image vulnerability test'){
            steps{
                sh ''
            }
        }
        
        stage('push to dockerhub'){
            steps{
                sh ''
            }
        }
        
        stage('pull image server'){
            steps{
                sh ''
            }
        }
        
        stage('DAST'){
            steps{
                sh ''
            }
        }
    }
}
