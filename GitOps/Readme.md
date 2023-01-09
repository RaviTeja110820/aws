# Deploy To Kubernetes with Jenkins GitOps GitHub Pipeline
we create a Jenkins pipeline with GitOps to deploy code into a Kubernetes cluster. CI part is done via Jenkins and CD part via ArgoCD (GitOps).

Gitops Perodically syncs the running cluster with desired state in Git Repo.


# Steps
1. GitOps Flow
2. Jenkins Installation
3. Jenkins jobs Setup
4. ArgoCD(GitOps) Installation
5. ArgoCD(GitOps) Setup
6. Automating GitHub to jenkins using webhook
7. Zero touch end to end (nirvana!)

# Setup

## GitOps Flow
![GitOps Flow](./images/gitopsflow.jpg)