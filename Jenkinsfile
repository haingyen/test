pipeline {
    agent {
        label 'ec2-agent'
    }

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-token')
        DOCKER_IMAGE = "haingyen/myrepo"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('info') { 
            steps {
                sh(script: """ whoami;pwd;ls -alt """, label: "first stage")
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-token') {
                        docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                    }
                }
            }
        }
        stage('deploy') { 
            steps {
                echo 'run container'
            }
        }
        stage('log') { 
            steps {
                echo 'check logs'
            }
        }
    }
}