pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
               checkout scm
            }
        }

        stage('Build & Tag Image') {
            steps {
                script {
                    sh 'docker build -t limarktest/nodejs-docker:$BUILD_NUMBER .'
                }
            }
        }
    }
}

