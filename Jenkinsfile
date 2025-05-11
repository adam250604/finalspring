pipeline {
    agent any

    stages {
        // Stage 1: Checkout from GitHub (automatically done by Jenkins SCM)
        stage('Checkout') {
            steps {
                git 'https://github.com/adam250604/finalspring.git'
            }
        }

        // Stage 2: Build with Maven
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        // Stage 3: SonarQube Analysis
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') { // Replace with your SonarQube server name
                    sh 'mvn sonar:sonar'
                }
            }
        }

        // Stage 4: Build Docker Image
        stage('Docker Build') {
            steps {
                script {
                    docker.build("your-docker-image-name:latest")
                }
            }
        }
    }

    // Post-build actions (optional)
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed! Check logs.'
        }
    }
}