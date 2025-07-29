pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'haingyen/test'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haingyen/test.git'
            }
        }
        stage('Builde docker image') {
            steps {
                echo "building docker image"
                sh "docker build -t ${DOCKER_HUB_REPO}:latest"
            }
        }
    }
}