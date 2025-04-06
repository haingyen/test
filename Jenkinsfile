pipeline {
    agent {
        label 'ec2-agent-01'
    }
    environment {
        IMAGE_NAME = 'haingyen/myrepo'
        TAG = 'latest'
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
                        credentialsId: 'docker-hub-token',
                        passwordVariable: 'DOCKER_HUB_PASSWORD',
                        usernameVariable: 'DOCKER_HUB_USER'
                    )]) {
                        sh('echo $DOCKER_HUB_PASSWORD | docker login --username $DOCKER_HUB_USER --password-stdin')
                    }
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-token') {
                        docker.image("${IMAGE_NAME}:${TAG}").push()
                    }
                }
            }
        }
    }
}