pipeline {
    agent {
        docker {
            image 'golang:1.22'
        }
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
