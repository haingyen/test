pipeline {
    agent any
    environment {
        IMAGE_NAME = 'haingyen/myrepo'
        TAG = '2.0.0'
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
            withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_HUB_TOKEN')]) {
                sh """
                    docker login -u haingyen -p ${DOCKER_HUB_TOKEN}
                    docker push ${IMAGE_NAME}:${TAG}
                """
            }
        }
    }
}
        // stage('Push') {
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