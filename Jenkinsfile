pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot application'
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image'
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
                echo 'Starting Docker container'

                bat 'docker run -d --name hello-rest-api -p 8080:8080 hello-rest-api:latest'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}
