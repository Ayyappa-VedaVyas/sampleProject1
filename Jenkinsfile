pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'git-token',
                    url: 'https://github.com/Ayyappa-VedaVyas/sampleProject1.git',
                    branch: 'main'
            }
        }

        stage('Build Images') {
            steps {
                bat 'docker-compose build'
            }
        }

        stage('Tag & Push') {
            steps {
                bat 'docker tag project_1-frontend vedavyas2498/frontend:v1'
                bat 'docker tag project_1-python vedavyas2498/backend:v1'
                bat 'docker push vedavyas2498/frontend:v1'
                bat 'docker push vedavyas2498/backend:v1'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker-compose up -d'
            }
        }
    }
}
