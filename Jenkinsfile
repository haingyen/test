pipeline {
    agent {
        label 'minikube'
    }

    environment {
        DOCKER_HUB_USER = "haingyen"
        DOCKER_REPO = "test"
        DOCKER_TAG = "0.3"
        DOCKER_IMAGE = "${DOCKER_HUB_USER}/${DOCKER_REPO}:${DOCKER_TAG}"
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
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
    }
}