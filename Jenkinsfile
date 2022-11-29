pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
               checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    sh 'docker build .'
                }
            }
        }
    }
}


