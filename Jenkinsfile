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

        stage('Archive') {
            steps {
                echo 'Archiving artifacts...'
                archiveArtifacts artifacts: 'build-artifact.txt', allowEmptyArchive: true
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh '''
                    # Example deployment script
                    # Stop the existing application
                    sudo systemctl stop myapp

                    # Copy the new application files
                    sudo cp -r ./myapp /opt/myapp

                    # Start the application
                    sudo systemctl start myapp

                    # Optionally, check the status
                    sudo systemctl status myapp
                '''
            }
        }

        stage('Notify Slack'){
            steps {
                script {
                    def artifactURL = "${env.JENKINS_URL}/job/${env.JOB_NAME}/${env.BUILD_NUMBER}/artifact/${artifactPath}"
                    //Add channel name
                    slackSend channel: 'mavenproject',
                    message: "Un nouveau build Java est disponible: ---> Resultat: ${currentBuild.currentResult}, Job: ${env.JOB_NAME}, Build: ${env.BUILD_NUMBER}"
                }
            }
        }
    

        
    }
}
