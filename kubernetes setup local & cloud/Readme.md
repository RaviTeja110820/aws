# kubernetes setup local & cloud

## Tools

1. `minikube` : local for testing
2. `kubeadm` : multi node cluster Local/Cloud (deployment tool)
3. `kops` : CLOUD AWS & GCP
4. `AWS EKS` : AWS Cloud Kubernetes Service

## minikube for Test Env

1. clone the source code :

   ```console
   $ git clone https://github.com/devopshydclub/vprofile-project.git
   $ git checkout kubernetes-setup
   $ cd minikube
   $ cat Minikube-commands.txt  # follow the commands in the file
   ```

2. now run the below

   ```console
   $ minikube.exe --help        # to verify minikube is installed 
   $ minikube start         # starts the local server
   $ kubectl get nodes       # you can see master node is ready
   $ cat .kube/config        # to see the cluster details
   ```

3. lets create a deployment

   ```console
   $ kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   $ kubectl.exe get pod
   $ kubectl.exe get deploy
   $ kubectl expose deployment hello-minikube --type=NodePort --port=8080  # expose it
   $ minikube service hello-minikube --url         # copy the url and paste in the browser
   ```

4. wrap up

   ```console
   $ kubectl.exe get svc
   $ kubectl.exe delete svc hello-minikube
   $ kubectl.exe get deploy
   $ kubectl.exe delete deploy hello-minikube
   $ minikube.exe stop
   $ minikube.exe delete
   ```

## kubeadm for cluster

### steps

1. Login to master & node with root user
2. Prerequisites on all nodes
3. Install Docker engine on all nodes
4. Install kubeadm, kubelet & kubectl
5. Execute kubeadm init -- on master node
6. save the node join command(kubeadm join...) returned by master node
7. Execute "kubeadm join" command returned by master setup, on Node
8. Execute user-setup script on Master node
9. Login to ubuntu user and run "kubectl get node"


### setup

1. run the below commands

   ```console
   $ git clone https://github.com/devopshydclub/vprofile-project.git
   $ git checkout kubernetes-setup
   $ cd kubeadm
   $ vagrant up
   $ vagrant ssh kubemaster
   $ kubectl get nodes
   $ kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   $ kubectl expose deployment hello-minikube --type=NodePort --port=8080
   $ kubectl get pod
   $ kubectl get deploy
   $ kubectl get svc
   $ kubectl describe pod pod_name
   $ exit
   $ vagrant destroy
   ```

## kops for cluster on AWS

### Prerequisites

* Domain for Kubernetes DNS records
* Create a linux VM and setup
  * kops,kubectl,ssh keys,aws cli
* Login to AWS account and setup
  * s3 bucket, IAM User for AWSCli, Route53 Hosted Zone


### setup.

1. launch an ec2 instance:
   * ubuntu 20
   * t2.micro
   * Name : Kops
   * security group : kops-sg

2. lets create an s3 Bucket , it stores the state of kops
   * Bucket Name : vprofile-kops-state

3. lets create an IAM user for AWS Cli
   * user name : kops admin
   * programmatic access
   * give admin access in attach policy

4. Goto Route 53
   * create hosted zone:
     * Domain name : kubevpro.devcan.in
     * public hosted zone
     * click on create
   * now add the ns records in godaddy

5. now login to the kops instance :

    ```console
    $ ssh-keygen     # public key should be sent to all the instances
    $ sudo apt update && sudo apt install awscli -y
    $ aws configure    # enter the iam user secret key
    ```

6. lets install kubectl from documentation

    ```console
    $ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"         # kubectl
    $ chmod +x ./kubectl  # giving executable permission
    $ sudo mv kubectl /usr/local/bin/  # so now we can access from any where
    $ kubectl --help     # to verify
    ```

7. install kubernetes from kops from documentation

    ```console
    $ curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
    $ sudo chmod +x kops-linux-amd64
    $ sudo mv kops-linux-amd64 /usr/local/bin/kops  # renaming kops-linux-amd64 to kops
    $ kops --help
    ```

8. to very domain name run the below command

    ```console
    $ nslookup -type=ns kubevpro.devcan.in
    ```

9. lets create cluster:

    ```console
    $ kops create cluster --name=kubevpro.devcan.in --state=s3://vprofile-kops-state --zones=us-east-2a,us-east-2b --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=kubevpro.devcan.in  # it creates configuration for the cluster in the s3 bucket
    $ kops update cluster --name kubevpro.devcan.in --state=s3://vprofile-kops-state --yes    # it creates cluster - 1 master and 2 worker nodes . wait for some time....
    ```

10. lets goto aws console -> ec2, you can see the instances created
11. to validate cluster run below command:

    ```console
    $ kops validate cluster --state=s3://vprofile-kops-state
    $ kubectl get nodes 
    ```

12. to delete cluster

    ```console
    $ kops delete cluster --name=kubevrpo.devcan.in --state=s3://vprofile-kops-state --yes
    ```

13. finally delete the hosted zone in aws console


## AWS EKS for the cluster

1. lets clone the repo:

    ```console
    $ git clone https://github.com/devopshydclub/vprofile-project.git
    $ cd eks/
    $ ls
    ```

2. run the below commands

    ```console
    $ vagrant up
    $ vagrant ssh
    $ aws --version
    $ eksctl version
    $ kubectl version
    ```

3. create an IAM user:
   * user name  : eksadmin
   * programmatic access
   * Attach policy : Administrator access

4. now run the below commands:

    ```console
    $ aws configure
    $ vim eks-cluster-setup.sh
    $ ./eks-cluster-setup.sh
    ```

5. in aws console you can check that new vpc is created
6. goto cloud formation and check
7. now goto eks
8. now run below commands
   
    ```console
    $ kubectl get nodes
    $ kubectl delete cluster vprofile-eks-cluster
    ```
