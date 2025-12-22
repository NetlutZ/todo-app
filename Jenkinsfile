pipeline {
    agent any

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
    }
}
