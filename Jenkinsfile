pipeline {
    agent {
        label 'slave-1-docker'   
    }


    stages {
        stage('Checkout Code') {
            steps {
                checkout scmGit(branches: [[name: 'email-notification']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/eayar123/trainmefordevsecops.git']])
            }
        }
    

        stage('SAST - sonarqube'){
            steps{
                withSonarQubeEnv('SonarCloud') { 
                    sh '''sonar-scanner \
                        -Dsonar.organization=trainmefordevsecops \
                        -Dsonar.projectKey=eayar-snake-devops-couse_trainmefordevsecops \
                        -Dsonar.sources=/home/ubuntu/jenkins/workspace/snake \
                        -Dsonar.host.url=https://sonarcloud.io'''

                }
                sh 'scan complete'
            }
                
        }
    
        
        stage('build') {
            steps{
                sh 'whoami'
                sh 'pwd'
                script {
                    app = docker.build("eayar/snake-eayar:${env.BUILD_ID}")
                }
            }
        }
        
        stage('image vulnerability test'){
            steps{
                sh ''
            }
        }
        
        stage('push to dockerhub'){
            steps{
                script {
                    docker.withRegistry( '', 'docker-hub-credentials' ) { 
                        app.push("${env.BUILD_ID}")
                        app.push("latest")
                    }   
                }
            }
        }
        
        stage('pull image server'){
            steps{
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
        
        stage('DAST'){
            steps{
                sh ''
            }
        }
    }
}
