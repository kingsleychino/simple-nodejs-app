pipeline {
    agent any

    tools {
        nodejs "NodeJS"   // Make sure you've installed & named a NodeJS tool in Jenkins global config
    }

    stages {
        stage('Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kingsleychino/simple-nodejs-app']]) 
               sh 'npm install'
            }
        }
    }

    stages {
        stage('Loggin to ECR') {
            steps {
               sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 503499294473.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
    }

    stages {
        stage('Build Docker Image') {
            steps {
               sh 'docker build -t simple-nodejs-app .'
            }
        }
    }

    stages {
        stage('Tag & Push to ECR') {
            steps {
               sh '''
                    docker tag simple-nodejs-app:latest 503499294473.dkr.ecr.us-east-1.amazonaws.com/simple-nodejs-app:latest
                    docker push 503499294473.dkr.ecr.us-east-1.amazonaws.com/simple-nodejs-app:latest
               '''
            }
        }
    }
}