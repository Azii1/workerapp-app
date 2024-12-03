pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'azii1/workerapp-app'
        DOCKER_TAG = 'latest' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git 'https://github.com/Azii1/workerapp-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t ${azii1/workerapp-app}:${latest} .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                echo 'Tagging Docker image...'
                sh 'docker tag ${azii1/workerapp-app}:${latest} ${azii1/workerapp-app}:${latest}'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                echo 'Logging into Docker Hub...'
                sh '''
                echo "${DOCKER_PASSWORD}" | docker login -u "${azii1}" --password-Cloud1234
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                sh 'docker push ${azii1/workerapp-app}:${latest}'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker logout'
        }
        success {
            echo 'Docker image successfully pushed to Docker Hub!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
