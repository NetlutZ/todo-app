pipeline {
    agent any

    tools {
       go '1.25.1'
    }

    environment {
        BACKEND_IMAGE  = "tilnel/todo-backend"
        FRONTEND_IMAGE = "tilnel/todo-frontend"
        TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'go version'
                sh 'go mod tidy'
                sh 'go build -o app'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t $BACKEND_IMAGE:$TAG .'
            }
        }

        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push $BACKEND_IMAGE:$TAG
                    '''
                }
            }
        }
    }
}
