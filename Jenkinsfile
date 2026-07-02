pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "atharva260/assignment4"
        TAG = "v1"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/godofthunder260240-collab/assignment4.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE:$TAG ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin"
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push $DOCKER_IMAGE:$TAG"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh "kubectl set image deployment/ass4 ass4=$DOCKER_IMAGE:$TAG"
            }
        }
    }
}
