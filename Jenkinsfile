pipeline {
    agent any // Use any available agent
    environment {
        // Define environment variables if needed
        PROJECT_NAME = 'SWasn'
    }
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm // Automatically uses the repository specified in Jenkins
            }
        }
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        // Unix-like systems (Linux, macOS)
                        sh './build.sh' // Assuming you have a build script
                    } else {
                        // Windows systems
                        bat 'build.bat' // Replace with relevant build steps for Windows
                    }
                }
            }
        }
        stage('Docker Build') {
            when {
                expression { isUnix() } // Docker is generally available on Unix systems
            }
            steps {
                script {
                    sh 'docker build -t ${PROJECT_NAME}:latest .'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    if (isUnix()) {
                        sh './deploy.sh staging' // Replace with your deploy script
                    } else {
                        bat 'deploy.bat staging' // Replace with equivalent deploy script for Windows
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs() // Clean workspace after the build
        }
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build or deployment failed. Check logs for details.'
        }
    }
}