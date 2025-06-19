pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token',
                    url: 'git https://github.com/Ayyappa-VedaVyas/sampleProject1.git',
                    branch: 'main'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Tag & Push') {
            steps {
                sh 'docker tag project_1-frontend vedavyas2498/frontend:v1'
                sh 'docker tag project_1-python vedavyas2498/backend:v1'
                sh 'docker push vedavyas2498/frontend:v1'
                sh 'docker push vedavyas2498/backend:v1'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
