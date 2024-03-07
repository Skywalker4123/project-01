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
                        mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=project-01 \
                          -Dsonar.host.url=http://3.110.30.112:9000 \
                          -Dsonar.login=sqp_637336592dddbfaac47bed437122eeaa8665f783
                    }
                }
            }
           
        }    
       
    }
}
