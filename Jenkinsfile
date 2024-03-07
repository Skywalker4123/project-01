pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }
    
    stages {        
        stage('CleanUp Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout from SCM') {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/Skywalker4123/project-01.git'
            }
        }
        stage('Build Application') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test Application') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package Application') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Sonarqube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner' // Assuming 'SonarScanner' is configured in Jenkins Global Tool Configuration
                    def sonar_token = 'sonar-token'
                    withSonarQubeEnv(credentialsId: 'sonar-token', installationName: 'SonarQube_Server') {
                        sh "${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=project-01 \
                        -Dsonar.sources=src \
                        -Dsonar.host.url=http://3.110.30.112:9000 \
                        -Dsonar.login=${sonar_token}"
                    }
                }
            }
           
        }    
       
    }
}
