pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }
    environment{
        APP_NAME = "project-01"
        RELEASE = "1.0.0"
        DOCKER_USER = "skywalker4123"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
        JENKINS_API_TOKEN = credentials("JENKINS_API_TOKEN")
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
                    waitForQualityGate abortpipeline: false, credentialsId: 'sonar-token'
                }
            }
           
        }
        stage('Build & Push Docker Image') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker', url: 'https://hub.docker.com') {
                    docker_image = docker build -t "${IMAGE_NAME}"
                    docker_image.push("${IMAGE_TAG}")
                    docker_image.push('latest')
                }

            }     
           
        }    
       
    }
}
