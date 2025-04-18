pipeline {
    agent {
        label "ec2-agent"
    }

    environment {
        DOCKER_HUB_USER = "haingyen"
        DOCKER_HUB_REPO = "${DOCKER_HUB_USER}/myrepo"
        DOCKER_IMAGE_TAG = "6.0.0"
        // DOCKER_BUILDKIT = "1"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haingyen/test.git'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_HUB_TOKEN')]) {
                    // sh """
                    //     # Đăng nhập Docker Hub bằng token
                    //     echo \$DOCKER_HUB_TOKEN | docker login -u ${DOCKER_HUB_USER} --password-stdin
                    // """
                    sh(""" echo \$DOCKER_HUB_TOKEN | docker login -u ${DOCKER_HUB_USER} --password-stdin """, label: "login dockerhub")
                }
            }
        }

        stage('Build') {
            steps {
                sh(""" docker build -t ${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG} . """, label: "build images")
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                // script {
                //     // Push image chính
                //     sh "docker push ${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG}"
                    
                //     // Push thêm tag nếu cần
                //     if (env.BRANCH_NAME == 'main' || env.BRANCH_NAME == 'master') {
                //         sh "docker push ${DOCKER_HUB_REPO}:${env.BUILD_NUMBER}"
                //     }
                // }
                sh(""" docker push ${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG} """, label: "push images")
            }
        }
        
        stage('Logout from Docker Hub') {
            steps {
                sh(""" docker logout """, label: "logout")
            }
        }
    }
    
    post {
        always {
            // Clean up workspace
            deleteDir()
            
            // Xóa image local để tiết kiệm dung lượng
            script {
                try {
                    sh "docker rmi ${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG}"
                    if (env.BRANCH_NAME == 'main' || env.BRANCH_NAME == 'master') {
                        sh "docker rmi ${DOCKER_HUB_REPO}:${env.BUILD_NUMBER}"
                    }
                } catch (e) {
                    echo "Failed to remove images: ${e}"
                }
            }
        }
        success {
            slackSend(
                channel: '#deployments',
                message: "Successfully pushed ${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG} to Docker Hub"
            )
        }
        failure {
            slackSend(
                channel: '#alerts',
                message: "Failed to push Docker image. Build: ${env.BUILD_URL}"
            )
        }
    }
}