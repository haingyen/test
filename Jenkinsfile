pipeline {
    agent any
    environment {
        IMAGE_NAME = 'haingyen/myrepo'
        TAG = '1.0.0'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }
        stage('Login') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: 'docker-hub-credentials',
                        passwordVariable: 'DOCKER_HUB_PASSWORD',
                        usernameVariable: 'DOCKER_HUB_USER'
                    )]) {
                        sh "echo $DOCKER_HUB_PASSWORD | docker login --username $DOCKER_HUB_USER --password-stdin"
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("${IMAGE_NAME}:${TAG}").push()
                    }
                }
            }
        }
    }
}