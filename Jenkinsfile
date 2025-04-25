pipeline {
    agent any

    environment {
        APP_DIR = '/opt/node-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/swathi6327/node-js-sample.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "No tests defined, skipping..."'
            }
        }

        stage('Deploy') {
            steps {
                // Stop previous instance if any
                sh 'pkill node || echo "No process to kill"'

                // Run app in background
                sh 'nohup node index.js > app.log 2>&1 &'
            }
        }
    }

    post {
        success {
            echo 'App deployed successfully!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
