pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'ellow0rld/k8s-demo'
    }
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/ellow0rld/K8s-Demo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-credentials-id') {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
