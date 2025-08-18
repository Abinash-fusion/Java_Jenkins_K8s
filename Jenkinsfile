pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    environment {
        DOCKER_HUB_REPO = 'abinashpati/java_jenkins_k8s'
		DOCKER_HUB_CREDENTIAL_ID='gitops-dockerhub'
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
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package' // This will create the target directory and the JAR
            }
        }
        stage('Docker Image Building') {
            steps {
                script {
                    echo 'building docker Image...'
                    dockerImage=docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }
        stage('Trivy Scan') {
            steps {
                echo 'scanning docker Image with Trivy...'
                //sh 'trivy image --no-progress --format json -o trivy-scan-report.txt ${DOCKER_HUB_REPO}:latest'
				sh 'trivy image --no-progress --skip-update --format json -o trivy-scan-report.txt ${DOCKER_HUB_REPO}:latest'
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    echo 'pushing docker Image to DockerHub...'
					docker.withRegistry("http://registry.hub.docker.com","${DOCKER_HUB_CREDENTIAL_ID}"){
					dockerImage.push('latest')
					}
                }
            }
        }
       stage('Install ArgoCD CLI'){
    steps {
        script { // Use a script block to execute Groovy code
		docker.image('argoproj/argocd:latest').inside {
		sh 'argocd version'
		sh 'argocd version'
                sh 'argocd login localhost:8080 --insecure --plaintext'
	
}
} 
