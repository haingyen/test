pipeline {
    agent any
    
    environment {
        KUBE_CONFIG = credentials('kubeconfig')
        DEPLOYMENT_NAME = 'nginx-deployment'
        NAMESPACE = 'default'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo.git'
            }
        }
        stage('Deploy to Minikube') {
            steps {
                script {
                    // Áp dụng các file cấu hình Kubernetes
                    sh "kubectl apply -f deployment.yaml --kubeconfig=${KUBE_CONFIG}"
                    // sh "kubectl apply -f service.yaml --kubeconfig=${KUBE_CONFIG}"
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                script {
                    sh "kubectl rollout status deployment/${DEPLOYMENT_NAME} --namespace=${NAMESPACE} --kubeconfig=${KUBE_CONFIG}"
                    sh "kubectl get pods --namespace=${NAMESPACE} --kubeconfig=${KUBE_CONFIG}"
                }
            }
        }
    }
}