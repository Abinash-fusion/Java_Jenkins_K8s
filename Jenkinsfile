pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    stages {
        stage('Checkout GitHub') {
            steps {
                git branch: 'main', credentialsId: 'GitOps-token', url: 'https://github.com/Abinash-fusion/Java_Jenkins_K8s.git'
            }
        }
        stage('installing node dependencies') {
            steps {
                sh 'echo "npm install..."'
            }
        }
        stage('Docker Image Building') {
            steps {
                script {
                    echo 'building docker Image...'
                }
            }
        }
        stage('Trivy Scan') {
            steps {
                echo 'scanning docker Image with Trivy...'
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    echo 'pushing docker Image to DockerHub...'
                }
            }
        }
        stage('Install ArgoCD CLI') {
            steps {
                sh 'echo "Installing argoCD cli..."'
            }
        }
    }
}
