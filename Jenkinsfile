pipeline {
    agent any

    environment {
        IMAGE_NAME = "java-maven-app"
        CONTAINER_NAME = "java-maven-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh '''
                docker run -d \
                  --name $CONTAINER_NAME \
                  -p 8080:8080 \
                  $IMAGE_NAME
                '''
            }
        }
    }
}
