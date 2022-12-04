pipeline {
	
	environment {
    imagerepo = 'limarktest'
    imagename = 'nodejs-docker'
	}

	agent any
	
	stages {
	
    stage('Build Docker Image') {
      steps {
        sh "docker build --no-cache . -t ${imagename}:v${BUILD_NUMBER}"
      }
    }
    
    stage('Tag Docker Image') {
      steps {
        sh "docker tag nodejs-docker:v${BUILD_NUMBER} ${imagerepo}/${imagename}:v${BUILD_NUMBER}"
      }
    }
    
    stage('Push Docker Image to Docker Hub') {
      steps {
        withDockerRegistry([ credentialsId: 'DockerHubCredentials', url: '' ]) {
          sh "docker push ${imagerepo}/${imagename}:v${BUILD_NUMBER}"
        }
      }
    }
    
    stage('Remove Docker Image') {
      steps{
        sh "docker rmi ${imagename}:v${BUILD_NUMBER}"
        sh "docker rmi ${imagerepo}/${imagename}:v${BUILD_NUMBER}"
      }
    }
    
    stage('Update Manifest') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'GitHubCredentials', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          sh "rm -rf gitops-demo-deployment"
          sh "git clone https://github.com/dinushchathurya/gitops-demo-deployment.git"
          sh "cd gitops-demo-deployment"
          dir('gitops-demo-deployment') {
            sh "sed -i 's/newTag.*/newTag: v${BUILD_NUMBER}/g' kustomize/overlays/*/*kustomization.yaml"
            sh "git config user.email ci@dinush.com"
            sh "git config user.name devops-bot"
            sh "git add ${WORKSPACE}/gitops-demo-deployment/kustomize/overlays/*/*kustomization.yaml"
            sh "git commit -m 'Update image version to: ${BUILD_NUMBER}'"
            sh"git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/dinushchathurya/gitops-demo-deployment.git HEAD:master -f"
          }
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

