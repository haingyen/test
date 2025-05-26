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
        stage('Apply Kubernetes Manifests & Sync App with ArgoCD'){
			steps {
				script {
					withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'kubeconfig', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://127.0.0.1:51475') {
                            sh "argocd login https://localhost:32187/ --username admin --password $(kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath='{.data.password}' | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }) --insecure"
                    }
				}
			}
		}
    }
}