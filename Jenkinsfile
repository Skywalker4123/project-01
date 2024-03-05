pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }

    stages {        
        stage('Source Code Repository') {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/Skywalker4123/project-01.git'
            }
        }
        stage('Compile Code') {
            steps {
                sh 'mvn compile'
            }
        }
    }
}