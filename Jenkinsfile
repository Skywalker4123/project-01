pipeline {
    agent any

    tools{
        jdk 'java17'
        maven 'maven3'
    }

    stages {
        stage('Work Space Cleaing') {
            steps {
                cleanws{}
            }
        }
        stage('Source Code Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Skywalker4123/project-01.git'
            }
        }
    }
}