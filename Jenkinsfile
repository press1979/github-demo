pipeline {
    agent any
    environment {
        // Change this path to any folder on your computer representing the "Live Server"
        DEPLOY_PATH = 'C:/live-website' 
    }
    stages {
        stage('1. Checkout Code') {
            steps {
                echo 'Pulling the latest code from GitHub...'
                checkout scm
            }
        }
        stage('2. Continuous Integration (Test)') {
            steps {
                echo 'Running Quality Checks...'
                // Simple CI Test: Check if the index.html file actually exists
                script {
                    if (fileExists('index.html')) {
                        echo 'SUCCESS: index.html found. Code structure is valid.'
                    } else {
                        error 'FAILURE: index.html is missing! Stopping pipeline.'
                    }
                }
            }
        }
        stage('3. Continuous Deployment (Deploy)') {
            steps {
                echo "Shipping code to the Live Server..."
                // Copies the fresh file into your simulated deployment web folder
                // Use 'cp' instead of 'copy' if you are running Jenkins on Linux/Mac
                bat "copy index.html \"${DEPLOY_PATH}\" /Y" 
                echo "Deployment Complete! Open your folder to see the updated site."
            }
        }
    }
}
