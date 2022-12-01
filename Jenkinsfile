pipeline {

    environment {
        imageName = 'limarktest/nodejs-docker'
    }

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
                    sh 'docker build -t $imageName:$BUILD_NUMBER .'
                }
            }
        }

        // stage('Pus Docker Image to Docker Hub') {
        //     steps {
        //         withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
        //             script {
        //                 def 'docker pudef $imageName:$BUILD_NUMBER'
        //             }
        //         }
        //     }
        // }

        // stage('Remove Docker Image') {
        //     steps{
        //         def 'docker rmi $imageName:$BUILD_NUMBER'
        //     }
        // }

        // stage('Update Manifest') {
        //     steps {
        //         script {
        //             git config user.email admin@example.com
        //         }
        //     }
        // }
    }

    post { 
        always { 
            cleanWs()
        }
    }

}
