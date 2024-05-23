pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ImAdSamadi/CF-DevOps.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Add your build steps here
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                // Add your test steps here
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                // Add your deploy steps here
                echo 'Deploying...'
            }
        }
    }

    post {
        always {
            // Add steps that should always run after the pipeline, like sending notifications
            echo 'Pipeline finished.'
        }
    }
}
