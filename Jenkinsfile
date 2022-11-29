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
                   docker build . 
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Publish') {
            steps {
                echo 'Publishing..'
            }
        }
        stage('Cleanup') {
            steps {
                echo 'Cleaning..'
            }
        }
    }
}

