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
                sh '''
                    ls
                    pwd
                '''

                withSonarQubeEnv('SonarCloud') { 
                    sh '''export SONAR_SCANNER_VERSION=4.7.0.2747
                        export SONAR_SCANNER_HOME=$HOME/.sonar/sonar-scanner-$SONAR_SCANNER_VERSION-linux
                        curl --create-dirs -sSLo $HOME/.sonar/sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-$SONAR_SCANNER_VERSION-linux.zip
                        unzip -o $HOME/.sonar/sonar-scanner.zip -d $HOME/.sonar/
                        export PATH=$SONAR_SCANNER_HOME/bin:$PATH
                        export SONAR_SCANNER_OPTS='-server'
                        
                        sonar-scanner \
                        -Dsonar.organization=trainmefordevsecops \
                        -Dsonar.projectKey=eayar-snake-devops-couse_trainmefordevsecops \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=https://sonarcloud.io
                        '''

                }
                
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
