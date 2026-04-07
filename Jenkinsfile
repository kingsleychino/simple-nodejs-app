pipeline {
    agent any

    tools {
        nodejs 'NodeJS18'
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
                sh 'npm test || true'
            }
        }

        stage('Build') {
            steps {
                sh '''
                if npm run | grep -q "build"; then
                  npm run build
                else
                  echo "No build script found, skipping..."
                fi
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/dist/**', allowEmptyArchive: true, fingerprint: true
            junit allowEmptyResults: true, testResults: '**/test-results/*.xml'
        }
    }
}
