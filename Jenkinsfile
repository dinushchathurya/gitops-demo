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
                    sh "docker build --no-cache . -t ${imagename}:${BUILD_NUMBER}"
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    sh "docker tag nodejs-docker:${BUILD_NUMBER} ${imagerepo}/${imagename}:${BUILD_NUMBER}"
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
                    script {
                        sh "docker push ${imagerepo}/${imagename}:${BUILD_NUMBER}"
                    }
                }
            }
        }

        stage('Remove Docker Image') {
            steps{
                sh "docker rmi ${imagename}:${BUILD_NUMBER}"
                sh "docker rmi ${imagerepo}/${imagename}:${BUILD_NUMBER}"
            }
        }

        stage('Update Manifest') {
            steps {
                script {
                    sh "sed -i 's|\$limarktest/nodejs-docker:latest | ${imagerepo}/${imagename}:${BUILD_NUMBER}|g' deployment.yml"
                    sh "git config user.email admin@example.com"
                    sh "git config user.name example"
                    sh "git add ."
                    sh "git commit -m 'Triggered Build: ${BUILD_NUMBER}'"
                    sh "git push https://github.com/dinushchathurya/gitops-demo-deployment.git"
                }
                // script { 
                //     bat '''
                //         git config user.email "build@gmail.com"
                //         git config user.name "build"
                //         git add . 
                //         git commit -m "Update app image tag to ${BUILD_NUMBER}"
                //         git remote set-url origin https://github.com/dinushchathurya/gitops-demo-deployment.git
                //         git push HEAD:master --force
                //     '''
                // }
            }
        }
    }

}