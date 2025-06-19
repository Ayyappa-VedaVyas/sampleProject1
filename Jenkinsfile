pipeline {
    agent any

    environment {
        DOCKER_HUB_NAMESPACE = 'vedavyas2498'
        FRONTEND_IMAGE = "${DOCKER_HUB_NAMESPACE}/frontend:v1"
        BACKEND_IMAGE = "${DOCKER_HUB_NAMESPACE}/backend:v1"
    }

    stages {

        stage('Checkout') {
            steps {
                git credentialsId: 'git-token', url: 'https://github.com/Ayyappa-VedaVyas/sampleProject1.git', branch: 'main'
            }
        }

        stage('Build Images') {
            steps {
                bat 'docker-compose build'
            }
        }

        stage('Tag & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-token', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                        echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin
                        docker compose down
                        docker tag project_1-frontend %FRONTEND_IMAGE%
                        docker tag project_1-python %BACKEND_IMAGE%
                        docker push %FRONTEND_IMAGE%
                        docker push %BACKEND_IMAGE%
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment step can go here (e.g., docker-compose up -d on a remote server)'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Please check the logs above.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
    }
}
