pipeline {
    agent {
        label 'ec2-agent'
    }
    environment {
        IMAGE_NAME = 'haingyen/myrepo'
        TAG = '4.0.0'
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub-token')
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                 script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-token') {
                        docker.image("${IMAGE_NAME}:${TAG}").push()
                    }
                }
            }
        }
        stage('write text file') {
            steps {
                script {
                    sh """
                        echo 'test...' > test.txt
                    """
                }
            }
        }
        // stage('Push') {
        //DOCKER_HUB_TOKEN
        //     steps {
        //         script {
        //             docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
        //                 docker.image("${IMAGE_NAME}:${TAG}").push()
        //             }
        //         }
        //     }
        // }
    }
}