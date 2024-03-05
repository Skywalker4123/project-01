pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }

    stages {        
        stage('Source Code Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Skywalker4123/project-01.git'
            }
        }
    }
}