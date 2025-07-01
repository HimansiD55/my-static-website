// Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any // Runs on any available agent (in this case, the EC2 instance itself)

    environment {
        // Define the deployment path for Nginx
        DEPLOY_PATH = '/var/www/html' // Default Nginx web root on Amazon Linux/RHEL
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from Git...'
                git branch: 'main', url: 'https://github.com/HimansiD55/my-static-website.git'
                // If your repo is private, you'll need to configure credentials in Jenkins
            }
        }
        stage('Clean Deployment Directory') {
            steps {
                echo "Cleaning previous deployment in ${DEPLOY_PATH}..."
                // Clean existing files to ensure a fresh deployment
                sh "sudo rm -rf ${DEPLOY_PATH}/*"
            }
        }
        stage('Deploy Static Website') {
            steps {
                echo 'Deploying static website to Nginx...'
                // Copy all files from the Jenkins workspace to the Nginx web root
                // The 'current directory' for the Jenkinsfile is the workspace root
                sh "sudo cp -r . ${DEPLOY_PATH}"
                echo 'Deployment complete!'
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}