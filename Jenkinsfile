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
                environment {
                    SCANNER_HOME=tool 'sonarscanner'
                }
                withSonarQubeEnv('sonarserver') {
                    sh ''' $SCANNER_HOME/bin/sonarscanner -Dsonar.projectName=Project-01 \
                    -Dsonar.projectKey=Project-01 '''                
                }         
            }
           
        }    
       
    }
}
