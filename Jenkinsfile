pipeline {
    agent {
        label 'ec2-agent'
    }

    environment {}

    stages {
        stage('info') { 
            steps {
                sh(script: """ whoami;pwd;ls -al """, label: "first stage")
            }
        }
         stage('build and push') { 
            steps {
                echo 'build via docker and push image on dockerhub'
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