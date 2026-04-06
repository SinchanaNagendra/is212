pipeline {
    agent any
    environment {
        // Use the exact ID you created in Manage Jenkins > Credentials
        DOCKER_CREDS = 'dockerhub-creds' 
        DOCKERHUB_USER = 'sinchananagendra'
        APP_NAME = 'is212'
    }
    stages {
        stage('Build and Push') {
            steps {
                script {
                    // 1. Build the image locally
                    bat "docker build -t ${DOCKERHUB_USER}/${APP_NAME}:v${env.BUILD_NUMBER} ."
                    
                    // 2. Login using the credentials (this is the part that was failing)
                    bat "echo %DOCKER_CREDS_PSW% | docker login -u ${DOCKERHUB_USER} --password-stdin"
                    
                    // 3. Push to Docker Hub
                    bat "docker push ${DOCKERHUB_USER}/${APP_NAME}:v${env.BUILD_NUMBER}"
                    
                    // 4. Cleanup to save disk space
                    bat "docker rmi ${DOCKERHUB_USER}/${APP_NAME}:v${env.BUILD_NUMBER}"
                }
            }
        }
    }
}
