pipeline {
    agent any

    enviroment {
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
                script {
                    echo 'building docker image'
                    docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }
    }
}