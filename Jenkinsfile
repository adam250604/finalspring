pipeline {
    agent any

    environment {
        SONARQUBE_URL = 'http://192.168.33.10:9000'
        DOCKER_IMAGE = 'my-java-app'
    }

    stages {
        // Stage 1: Clone from GitHub
        stage('Checkout') {
            steps {
                git 'https://github.com/yourusername/your-repo.git'
            }
        }

        // Stage 2: Build with Maven
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        // Stage 3: SonarQube Analysis
        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=my-java-project'
                }
            }
        }

        // Stage 4: Docker Build
        stage('Docker Build') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${env.BUILD_ID}")
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}