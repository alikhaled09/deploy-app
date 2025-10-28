pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/alikhaled09/deploy-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t myflaskapp ./python-app-small'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop and remove any old container
                    sh 'docker rm -f flask-container || true'
                    
                    // Run new container
                    sh 'docker run -d -p 8000:8000 --name flask-container myflaskapp'
                }
            }
        }
    }
}
