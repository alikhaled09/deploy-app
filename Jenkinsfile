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
                    sh 'docker build -t myflaskapp .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh '''
                        docker rm -f flask-container || true
                        docker run -d -p 8000:8000 --name flask-container myflaskapp
                    '''
                }
            }
        }
    }
}
