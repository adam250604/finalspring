pipeline {
    agent any
    
    tools {
        maven 'M3'   // Must match Maven tool name in Jenkins
        jdk 'jdk17'  // Must match JDK tool name in Jenkins
    }
    
    stages {
        // Stage 1: Clone the repository
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/adam250604/finalspring.git'
            }
        }
        
        // Stage 2: Build with Maven
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        
        // Stage 3: Run SonarQube analysis
        stage('SonarQube Analysis') {


            steps {
                withSonarQubeEnv('SonarQube') { 
                    sh 'mvn sonar:sonar -Dsonar.projectKey=finalspring -Dsonar.host.url=http://localhost:9000'
                }
            }
        }


        
        // Stage 4: Build Docker image
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("spring-boot-app:${env.BUILD_ID}")
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline completed. Check logs for details.'
        }
    }
}