pipeline {
    agent any

    tools {
        nodejs "NodeJS"   // Make sure you've installed & named a NodeJS tool in Jenkins global config
    }

    stages {
        stage('Checkout') {
            steps {
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kingsleychino/simple-nodejs-app']]) 
            }
        }
    }
}