pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
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
                withSonarQubeEnv('SonarQube') {
                withCredentials([string(credentialsId: 'SonarQube-Token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=project-01 \
                    -Dsonar.host.url=http://3.110.30.112:9000 \
                    -Dsonar.login=$SONAR_TOKEN 
                    '''
                }
            }
        }
    }
}