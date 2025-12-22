pipeline {
    agent any

    tools {
       go 'go-1.25.1'
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
    }
}
