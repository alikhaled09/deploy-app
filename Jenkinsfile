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
                    // Build using repository root Dockerfile. Use isUnix() to support Windows agents.
                    if (isUnix()) {
                        sh 'docker build -t myflaskapp .'
                    } else {
                        bat 'docker build -t myflaskapp .'
                    }
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop and remove any old container
                    // Attempt to remove existing container; ignore errors if it doesn't exist.
                    try {
                        if (isUnix()) {
                            sh 'docker rm -f flask-container'
                        } else {
                            bat 'docker rm -f flask-container'
                        }
                    } catch (err) {
                        echo 'No existing container to remove'
                    }
                    
                    // Run new container (platform-specific runner)
                    if (isUnix()) {
                        sh 'docker run -d -p 8000:8000 --name flask-container myflaskapp'
                    } else {
                        bat 'docker run -d -p 8000:8000 --name flask-container myflaskapp'
                    }
                }
            }
        }
    }
}
