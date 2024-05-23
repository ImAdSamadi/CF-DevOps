pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                // git url: 'https://github.com/ImAdSamadi/CF-DevOps.git', branch: 'main'
                sh "git clone https://github.com/ImAdSamadi/CF-DevOps.git"
                
            }
        }

        stage('Build') {
            steps {
                // Add your build steps here
                echo 'Building...'
                script {
                    
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                    
                    // Navigate to the directory containing the Maven project
                    dir('java-maven/maven') {
                        // Run Maven commands
                        sh 'mvn clean test package'
                    }
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
}
