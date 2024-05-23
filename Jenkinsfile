pipeline {
    agent any

    environment {
        // Define the base URL for Jenkins
        JENKINS_URL = 'http://192.168.37.128:8080'
    }
    
    stages {

        stage('Checkout') {
            steps {
                // clean the directory
                sh "rm -rf *"
                // Checkout the Git repository
                sh "git clone https://github.com/ImAdSamadi/CF-DevOps.git"
            }
        }
    

        stage('Build') {
            steps {
                // Here, we can can run Maven commands
                script {
                    
                    def currentDir = pwd()
                    echo "Current directory: ${currentDir}"
                    
                    // Navigate to the directory containing the Maven project
                    
                    dir('java-maven/maven') {
                        //sh 'mvn clean test package'
                        //sh "java -jar target/maven-0.0.1-SNAPSHOT.jar"
                    }
                    
                   
                }
            }
        }

         stage('Archive') {
            steps {
                // Archive the JAR files generated by Maven
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh '''
                    # Define variables for paths
                    APP_NAME="CF-DevOps"
                    BUILD_ARTIFACT="build-artifact.zip"
                    DEPLOY_DIR="/opt/$CF-DevOps"
                    BACKUP_DIR="/opt/${CF-DevOps}_backup"
                    
                    # Stop the existing application
                    sudo systemctl stop $CF-DevOps
                    
                    # Backup current application
                    if [ -d "$CF-DevOps" ]; then
                        sudo mv $DEPLOY_DIR $BACKUP_DIR
                    fi
                    
                    # Create new deployment directory
                    sudo mkdir -p $DEPLOY_DIR
                    
                    # Unzip and copy the new application files
                    sudo unzip $BUILD_ARTIFACT -d $DEPLOY_DIR
                    
                    # Set the appropriate permissions
                    sudo chown -R $USER:$USER $DEPLOY_DIR
                    
                    # Start the application
                    sudo systemctl start $CF-DevOps
                    
                    # Optionally, check the status
                    sudo systemctl status $CF-DevOps
                '''
            }
        }

        stage('Notify Slack'){
            steps {
                script {
                    def artifactPath = "java-maven/maven/target/maven-0.0.1-SNAPSHOT.jar"
                    def artifactURL = "${env.JENKINS_URL}/job/${env.JOB_NAME}/${env.BUILD_NUMBER}/artifact/${artifactPath}"
                    
                    //Add channel name
                    slackSend channel: 'mavenproject',
                    message: "Un nouveau build Java est disponible: ---> Resultat: ${currentBuild.currentResult}, Job: ${env.JOB_NAME}, Build: ${env.BUILD_NUMBER}"
                }
            }
        }
    

        
    }
}
