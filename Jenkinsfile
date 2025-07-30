pipeline {
    agent any

    stages {
        stage('Initialize') {
            steps {
                echo 'Starting FastAPI CI/CD Pipeline...'
                sh '''
                    python -m venv myenv
                    . myenv/bin/activate
                    pip install --upgrade pip
                '''
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bmuia/jenkins-project.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                    . myenv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run FastAPI') {
            steps {
                sh '''
                    . myenv/bin/activate
                    uvicorn main:app --host 0.0.0.0 --port 8000 &
                '''
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'pkill -f uvicorn || true'  // Use `|| true` to avoid failure if process not found
        }
    }
}
