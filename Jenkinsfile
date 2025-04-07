pipeline {
    agent {
        any
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-token')
        IMAGE_NAME = 'haingyen/myrepo'
        TAG = '1.0.0'
    }
    stages {
        stage('Build') {
            steps {
                sh('docker build -t $IMAGE_NAME:$TAG .')
            }
        }
        stage('Login') {
            steps {
                sh('echo $DOCKERHUB_CREDENTIALS_PASSWORD | docker login --username $DOCKERHUB_CREDENTIALS_USER --password-stdin')
            }
        }
        stage('Push') {
            steps {
                sh('docker push $IMAGE_NAME:$TAG')
            }
        }
    }
    post {
        always {
            sh('docker logout')
        }
    }
}