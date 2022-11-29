pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
               checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/dinushchathurya/gitops-demo']]])
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

