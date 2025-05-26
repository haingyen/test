pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    environment {
        DOCKER_IMAGES = 'haingyen/myrepo'
        DOCKER_HUB_CREDENTIALS_ID = 'dockerhub-token'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haingyen/test.git'
            }
        }
        stage('Install Depens') {
            steps {
                sh "npm install"
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    echo 'building docker images'
                    dockerImage = docker.build("${DOCKER_IMAGES}:latest")
                }
            }
        }
        stage('Push Docker Images on Dockerhub') {
            steps {
                script {
                    echo 'Push Docker Images on Dockerhub'
                    docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_HUB_CREDENTIALS_ID}") {
                        dockerImage.push('latest')
                    }
                }
            }
        }
        stage('Install Argocd CLI') {
            steps {
                sh '''
                    echo 'Install Argocd CLI'
                    curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
                    sudo apt install -y argocd-linux-amd64
                    chmod +x /usr/local/bin/argocd
                '''
            }
        }
    }
}