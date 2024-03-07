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
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
           
        }    
       
    }
}
