pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bmuia/jenkins-project.git'

            }
        }

        stage('Install dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run FastAPI') {
            steps {
                sh 'uvicorn main:app --host 0.0.0.0 --port 8000 &'
            }
        }
    }
}

    post {
        always {
            echo 'Cleaning up...'
            sh 'pkill -f uvicorn' // Stop the FastAPI server
        }
    }

// This Jenkinsfile defines a simple CI/CD pipeline for a FastAPI application.
// It checks out the code from a Git repository, installs dependencies, and runs the FastAPI
// server using Uvicorn. The server runs in the background, and after the pipeline completes,
// it cleans up by stopping the Uvicorn server process.