pipeline {

    agent any

    stages {

        stage('Check Java') {
            steps {
                bat 'java -version'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/connectwithuma2025-alt/hello-rest-api.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t hello-rest-api:latest .'
            }
        }

        stage('Docker Stop Old Container') {
            steps {
                bat 'docker stop hello-rest-api || exit 0'
                bat 'docker rm hello-rest-api || exit 0'
            }
        }

        stage('Docker Run') {
            steps {
                bat 'docker run -d --name hello-rest-api -p 8080:8080 hello-rest-api:latest'
            }
        }
    }

    post {
        success {
            echo 'BUILD + TEST + DOCKER DEPLOYMENT SUCCESSFUL'
        }

        failure {
            echo 'Pipeline failed'
        }
    }
}