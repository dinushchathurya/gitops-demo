pipeline {

    environment {
        imagename = 'limarktest/nodejs-docker'
        imagetag  =  "$imagetag"
    }

    agent any

    stages {

        stage('Build & Tag Image') {
            steps {
                script {
                    bat 'docker build -t $imagename:$imagetag .'
                }
            }
        }

        stage('Pus Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
                    script {
                        bat 'docker pudef $imagename:$imagetag'
                    }
                }
            }
        }

        stage('Remove Docker Image') {
            steps{
                bat 'docker rmi $imagename:$imagetag'
            }
        }

        stage('Update Manifest') {
            steps {
                script {
                    bat 'git config user.email admin@example.com'
                    bat 'git config user.name example'
                    bat 'git add .'
                    bat 'git commit -m 'Triggered Build: $imagetag''
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
