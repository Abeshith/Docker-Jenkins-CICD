ipipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIAL_ID = 'docker-cred'
        DOCKERHUB_REGISTRY = 'https://registry.hub.docker.com'
        DOCKERHUB_REPOSITORY = 'abeshith/flaskapp-cicd'
    }

    stages {
        stage('Checkout') {
            steps {
                 script {
                    echo 'Checkout Git...'
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'mlops-git', url: 'https://github.com/Abeshith/Docker-Jenkins-CICD.git']])
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                 script {
                    echo 'Building Docker image...'
                    dockerImage = docker.build("${DOCKERHUB_REPOSITORY}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    echo 'Pushing Docker image...'
                    docker.withRegistry("${DOCKERHUB_REGISTRY}","${DOCKERHUB_CREDENTIAL_ID}"){
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
