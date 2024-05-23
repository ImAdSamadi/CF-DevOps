pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                 git url: 'https://github.com/ImAdSamadi/CF-DevOps.git', branch: 'main'

                
            }
        }
    

        stage('Build') {
            steps {
                // Add your build steps here
                echo 'Building...'
                script {
                    
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                    
                }
            }
        }

        
    }
}
