# Java App Deployment on Kubernetes Cluster

## steps

1. Kubernetes cluster
2. Containerized apps
3. Create EBS volume for DB pod
4. LABEL Node with zones names
5. Kubernetes Defination files for :
   * Deployment
   * Service
   * Secret
   * Volume

## setup

### lets create kubernetes cluster using kops

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

8. to verify domain name run the below command

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

### ebs volume for mysql

1. run the below command:

   ```console
   $ aws ec2 create-volume --availability-zone=us-east-2a --size=3 --volume-type=gp2     # copy the volume id and save it
   $ kubectl get nodes --show-labels
   $ kubectl get nodes
   $ kubectl describe node name_of_worker_node | grep us-east-2
   $ kubectl label nodes name_of_worker_node zone=us-east-2a   # we are labelling thats it
   $ kubectl describe other_node name_of_worker_node | grep us-east-2
   $ kubectl label nodes name_of_worker_node zone=us-east-2b
   ```

### kube secret for passwords

   ```console
   $ git clone 
   $ echo -n "vprodbpass" | base64     # copy the encoded password of db. paste it in app-secret.yml
   $ echo -n "guest" | bse64  # copy the encoded password of rabbit_mq. paste it in app-secret.yml
   $ kubectl create -f app-secret.yaml
   $ Kubectl get secret
   $ kubectl describe secret
   ```

### DB Deployment Definition

earlier we created a ebs volume of 3 GB . we need to attach a tag to it. GoTO volumes in aws console. Select the volume that matches with our volume id that saved eralier. click on tags -> Add tag -> Key : KubernetesCluster, Value : vprokube.devcan.in . we need give our cluster name there.

```console
$ kubectl create -f vprodbdep.yml
$ kubectl get deploy
$ kubectl get pod
$ kubectl describe pod pod_name     # you can find any errors here if you get
$ kubectl get pod
```

### to execute all defination files

```console
$ kubectl create -f .
$ kubectl get deploy
$ kubectl get pod 
$ kubectl get svc            # copy the load balancer endpoint and paste in browser
$ kubectl delete -f .
$ kops delete cluster --name
```