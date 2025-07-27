pipeline {
    agent any
    
    environment {
        DEPLOYMENT_NAME = 'nginx-deployment'
        NAMESPACE = 'default'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haingyen/test.git'
            }
        }
        // stage('Test Kubernetes') {
        //     steps {
        //         script {
        //             sh 'kubectl get pods'
        //         }
        //     }
        // }
        stage('Deploy to Minikube') {
            steps {
                 withCredentials([file(credentialsId: 'minikube', variable: 'KUBECONFIG')]) {
                     // Thực thi kubectl
                    sh 'kubectl apply -f deployment.yaml --kubeconfig=$KUBECONFIG'
                }
            }
        }
        
        // stage('Verify Deployment') {
        //     steps {
        //         script {
        //             sh "kubectl rollout status deployment/${DEPLOYMENT_NAME} --namespace=${NAMESPACE} --kubeconfig=${KUBE_CONFIG}"
        //             sh "kubectl get pods --namespace=${NAMESPACE} --kubeconfig=${KUBE_CONFIG}"
        //         }
        //     }
        // }
    }
}