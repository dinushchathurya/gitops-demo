pipeline {

    environment {
        imagerepo = 'limarktest'
        imagename = 'nodejs-docker'
        imagetag  =  "$imagetag"
    }

    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    bat 'docker build -t ${imagename} .'
                }
            }
        }
        
        stage('Tag Docker Image') {
            steps {
                script {
                    bat 'docker tag ${imagename}:latest ${imagerepo}/${imagename}:${imagetag}'
                }
            }
        }

        stage('Pus Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
                    script {
                        bat 'docker push $imagename:$imagetag'
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
