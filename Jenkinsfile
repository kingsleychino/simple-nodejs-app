pipeline {
    agent any

    tools {
        nodejs 'NodeJS18' // Must match the name configured in Jenkins > Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kingsleychino/simple-nodejs-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Outputs JUnit-compatible XML if jest-junit or mocha-junit-reporter is configured
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build' // Remove if there's no build script in package.json
            }
        }
    }

    post {
        always {
            // Archive any build output or dist folder
            archiveArtifacts artifacts: '**/dist/**', allowEmptyArchive: true, fingerprint: true

            // Only include this if your test runner outputs JUnit XML
            junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
        }
    }
}
