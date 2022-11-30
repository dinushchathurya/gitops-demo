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

        // stage('Build & Tag Image') {
        //     steps {
        //         script {
        //             def 'docker build -t $imageName:$BUILD_NUMBER .'
        //         }
        //     }
        // }

        // stage('Pus Docker Image to Docker Hub') {
        //     steps {
        //         withDockerRegistry([ credentialsId: "DockerHubCredentials", url: "" ]) {
        //             script {
        //                 def 'docker pudef $imageName:$BUILD_NUMBER'
        //             }
        //         }
        //     }
        // }

        // stage('Remove Docker Image') {
        //     steps{
        //         def "docker rmi $imageName:$BUILD_NUMBER"
        //     }
        // }

        stage('Update Manifest') {
           steps {
                script {
                    def "git config user.email admin@example.com"
                    def "git config user.name example"
                    def "git add ."
                    def "git commit -m 'feat: Triggered Build: ${env.BUILD_NUMBER}'"
                    // sh "git push https://${GIT_USERNAME}:${encodedPassword}@github.com/${GIT_USERNAME}/example.git"
                    def "https://github.com/dinushchathurya/gitops-demo/"
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
