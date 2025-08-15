pipeline {
    agent any
    stages {
        stage('Checkout GitHub') {
            steps {
                git branch: 'main', credentialsId: 'GitOps-token', url: 'https://github.com/Abinash-fusion/Java_Jenkins_K8s.git'
            }
        }
    }
}
