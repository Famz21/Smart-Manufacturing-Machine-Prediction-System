pipeline {
    agent any
    environtment {
        DOCKER_HUB_REPO = "viraz21/gitops-project"
        DOCKER_HUB_CREDENTIALS_ID = "gitops-dockerhub-token"
    }
    stages {
        stage('Checkout Github') {
            steps {
                echo 'Checking out code from GitHub...'
		        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/Famz21/Smart-Manufacturing-Machine-Prediction-System.git']])
		    }
        }        
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image ...'
                    dockerImage = docker.build("${DOCKER_HUB_REPO}:latest")
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    echo 'Pushing Docker image to DockerHub...'
                    docker.withRegistry('https://registry.hub.docker.com', "${DOCKER_HUB_CREDENTIALS_ID}") {
                       dockerImage.push('latest') 
                    }
                }
            }
        }
        stage('Install Kubectl & ArgoCD CLI') {
            steps {
                echo 'Installing Kubectl and ArgoCD CLI...'
            }
        }
        stage('Apply Kubernetes & Sync App with ArgoCD') {
            steps {
                echo 'Applying Kubernetes and syncing with ArgoCD...'
            }
        }
    }
}
