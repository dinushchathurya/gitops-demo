pipeline {

    environment {
        imagename = 'limarktest/nodejs-docker'
    }

    agent any

    stages {

        stage('Build & Tag Image') {
            steps {
                script {
                    bat "docker build --no-cache . -t $imagename:${BUILD_NUMBER}"
                }
            }
        }

        stage('Pus Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
                    script {
                        bat 'docker push $imagename:${BUILD_NUMBER}'
                    }
                }
            }
        }

        stage('Remove Docker Image') {
            steps{
                bat 'docker rmi $imagename:${BUILD_NUMBER}'
            }
        }

        stage('Update Manifest') {
            steps {
                script {
                    bat 'git config user.email admin@example.com'
                    bat 'git config user.name example'
                    bat 'git add .'
                    bat 'git commit -m 'Triggered Build: ${env.BUILD_NUMBER}''
                    bat 'git push https://github.com/dinushchathurya/gitops-demo.git'
                }
            }
        }
    }

    post { 
        always { 
            cleanWs()
        }
    }

}
