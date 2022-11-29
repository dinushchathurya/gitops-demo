pipeline {

    environment {
        imageName = "limarktest/nodejs-docker"
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

        stage('Push Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: "DockerHubCredentials", url: "" ]) {
                    script {
                        sh 'docker push $imageName:$BUILD_NUMBER'
                    }
                }
            }
        }

        stage('Remove Docker Image') {
            steps{
                sh "docker rmi $imageName:$BUILD_NUMBER"
            }
        }


    }

    post { 
        always { 
            cleanWs()
        }
    }
}

