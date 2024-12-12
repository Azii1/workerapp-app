pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main',
                    url: 'https://github.com/Azii1/workerapp-app.git',
                    credentialsId: 'Github-credentials'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t my-app-image .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                echo 'Tagging Docker image...'
                sh 'docker tag my-app-image azii1/workerapp-app:latest'
            }
        }
        
        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'azii1', passwordVariable: 'dckr_pat_OuicC5FQgjNYBudH4JjFMmygxkM')]) {
                    sh 'echo "dckr_pat_OuicC5FQgjNYBudH4JjFMmygxkM" | docker login -u "azii1" --password-stdin'
                }
            }
        } 
        
        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image...'
                sh 'docker push azii1/workerapp-app:latest'
            }
        }
    }
}
