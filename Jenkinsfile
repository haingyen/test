pipeline {
    agent {
        label 'ec2-agent'
    }

    stages {
        stage('info') { 
            steps {
                sh(script: """ whoami;pwd;la -al """, label: "first stage")
            }
        }
    }
}