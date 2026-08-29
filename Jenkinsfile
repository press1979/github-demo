pipeline {
    agent any
    environment {
        // A standard folder on Linux that Jenkins always has permission to use
        DEPLOY_PATH = '/home/ubuntu/github-test' 
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
                
                // 1. Automatically create the folder if it doesn't exist yet
                sh "mkdir -p ${DEPLOY_PATH}"
                
                // 2. LINUX FIX: Use 'sh' and 'cp' to copy the website file
                sh "cp index.html ${DEPLOY_PATH}/"
                
                echo "Deployment Complete! File copied to ${DEPLOY_PATH}/index.html"
            }
        }
    }
}
