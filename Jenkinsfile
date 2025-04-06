pipeline {
    agent {
        label 'ec2-agent-01'
    }

    environment {
        DOCKER_IMAGE     = "haingyen/myrepo"
        DOCKER_IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haingyen/test.git'
            }
        }

        stage('Build image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}")
                }
            }
        }
         stage('Push on Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com/v2/', 'docker-hub-token') {
                        docker.image("${DOCKER_IMAGE}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}