# kubernetes setup local & cloud

## Tools

1. `minikube` : local for testing
2. `kubeadm` : multi node cluster Local/Cloud
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