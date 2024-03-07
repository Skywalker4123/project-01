pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME=tool 'SonarQube-Scanner'
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
                withSonarQubeEnv(credentialsId: 'SonarQube-Token') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=project-01 \
                    -Dsonar.projectKey=project-01 '''
                }
                }    
            }
        }
    }
}