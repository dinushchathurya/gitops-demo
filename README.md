## This repo contains the scripts and small NodeJS app to demonstrate GitOps example using Jenkins, Argocd & Kustomize

In this example, we will be using a simple NodeJS app to demonstrate the GitOps workflow. The app is a simple NodeJS app that returns the simple hello world. The app is deployed in a Kubernetes cluster and the deployment is managed by ArgoCD. The ArgoCD deployment is managed by Jenkins. The Jenkins pipeline is triggered by a commit to the GitOps repo. The GitOps repo contains the Kubernetes manifests and the Kustomize files to deploy the app.

### Jenkinsfile

This file contains the script which we need to build, tag, push image to DockerHub and update the manifest file, which we use to deploy our applcation k8 cluster using argocd application in the <a href="https://github.com/dinushchathurya/gitops-demo-deployment">gitops-demo-deployment repository</a> with new image tag

### Dockerfile

This file contains the Dockerfile to build the NodeJS app.

### Server.js

This file contains the NodeJS app code.