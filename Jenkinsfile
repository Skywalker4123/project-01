pipeline {
    agent any

    tools {
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
                        sh "mvn clean package sonar:sonar"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                script {
                    def qg = waitForQualityGate() // Corrected waitForQualityGate usage
                    if (qg.status != 'OK') {
                        error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
                }
            }
        }
        stage('Build & Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                        sh "docker build -t project-01 . "
                        sh "docker tag project-01 skywalker4123/project-01:latest"
                        sh "docker push skywalker4123/project-01:latest"
                    }    
                }
            }     
        }    
    }
}
