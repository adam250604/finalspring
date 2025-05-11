pipeline {
    agent any

    tools {
        maven 'M3'
        jdk 'jdk17'
    }

    environment {
        SONARQUBE_SERVER = 'SonarQube'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/adam250604/finalspring.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=finalspring -Dsonar.host.url=http://192.168.33.10:9000'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t finalspring:latest .'
            }
        }
    }
}
