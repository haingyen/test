pipeline {
    agent {
        label 'ec2-agent'
    }

    stages {
        stage('info') { 
            steps {
                sh(script: """ whoami;pwd;ls -al """, label: "first stage")
            }
        }
    }
}