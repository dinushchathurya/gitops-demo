pipeline {

    environment {
        imagerepo = 'limarktest'
        imagename = 'nodejs-docker'
    }

    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    bat "docker build --no-cache . -t nodejs-docker:${BUILD_NUMBER}"
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    bat "docker tag nodejs-docker:${BUILD_NUMBER} ${imagerepo}/${imagename}:${BUILD_NUMBER}"
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
                    script {
                        bat 'docker push ${imagerepo}/${imagename}:${BUILD_NUMBER}'
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
