# Deploy To Kubernetes with Jenkins GitOps GitHub Pipeline
we create a Jenkins pipeline with GitOps to deploy code into a Kubernetes cluster. CI part is done via Jenkins and CD part via ArgoCD (GitOps).

Gitops Perodically syncs the running cluster with desired state in Git Repo.


# Steps
1. GitOps Flow
2. Jenkins Installation
3. Install Docker
4. Jenkins jobs Setup
5. ArgoCD(GitOps) Installation
6. ArgoCD(GitOps) Setup
7. Automating GitHub to jenkins using webhook
8. Zero touch end to end (nirvana!)

# Setup

## GitOps Flow
![GitOps Flow](./images/gitopsflow.jpg)

## Jenkins Installation
To install jenkins switch branch to Jenkins Installation in same repositry or follow this link - https://github.com/RaviTeja110820/aws/tree/Devops-Projects/Jenkins%20Installation 

## Installing Docer on EC2
To get Docker running on the AWS AMI you should follow the steps below:

1. Update the packages on your instance
   ```console
   [ec2-user ~]$ sudo yum update -y
   ```
2. Install Docker
   ```console
   [ec2-user ~]$ sudo yum install docker -y
   ```
3. Start the Docker Service
   ```console
   [ec2-user ~]$ sudo service docker start
   ```
4. Add the ec2-user to the docker group so you can execute Docker commands without using sudo.
   ```console
   [ec2-user ~]$ sudo usermod -a -G docker ec2-user
   ```

## Jenkins jobs Setup
1. goto jenkins -> manage jenkins -> manage credentials -> Global credentials -> Add credentials:
    * username and password of dockerhub. ID = **dockerhub**
    * username of github, password should be generated- github-> settings -> developer settings -> personal access -> Generate new token : note - test gitops, select repo, select admin:repo_hook , select notification, Generate token, copy token and paste in jenkins github password. ID = **github**
2. New item -> name- buildimage, select pipeline.
    * **pipeline**-> pipeline script from SCM:
      * SCM - git , repositry url - https://github.com/saha-rajdeep/kubernetescode.git
      * branch - */main
    * save it 
3. New item -> name- updatemanifest, select pipeline.
   * This project is parameterized:
      * Name - DOCKERTAG
      * Default Value - latest
   * **pipeline**-> pipeline script from SCM:
      * SCM - git , repositry url - https://github.com/saha-rajdeep/kubernetesmanifest.git
      * branch - */main
   * save it 
4. Go to buildimage job and click on Build and go to updatemanifest job and check out. Also go to your dockerhub and refresh the page, Then you see new image.   