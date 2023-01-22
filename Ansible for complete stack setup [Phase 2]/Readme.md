# Ansbile For Complete stack Setup
In this project we will Provision an application on EC2 with Ansible

![Architecture](./images/architecture.jpg)

# ----
1. Setup VPC [secure & HA]
2. Provision Ec2 Instances,ELB,security grp
3. Provision Vprofile stack application on Ec2 instances.
   * Build Artifact
   * MySQL
   * Memcache
   * RabbitMQ
   * Tomcat
   * Nginx


# Steps
1. Login to AWS
2. Create ec2 instance to run ansible playbook
3. install Ansible
4. Install boto
5. Setup ec2 Role for ansible
6. Fetch Source code from project Ansible for AWS
7. Execute VPC playbook
8. Playbook to launch ec2, elb, security group for vprofile
9. Get into vprofile vpc
10. playbooks for vprofile stack setup


# Setup
1. sign in to aws console and click on launch instance:
    * name : controller
    * AMI : Ubuntu 20
    * Instance type : t2.micro
    * Security Group : ansible-sg -> ssh from myIP
    * Create a keypair : ansible-ohio-key
    * in advanced details -> provision , user data:
        ```console
        #!/bin/bash
        sudo apt update
        sudo apt install ansible -y
        ```
    * submit
2. connect to the instance and check the ansible version that was installed by running below command.
   ```console
   $ ansible --version
   ```
3. Now install boto in contrller instance.
   ```console
   $ sudo apt install python3-boto3 python3-botocore python3-boto -y
   ```
   > boto helps us to connect to aws services
4. Dont put access key and secret access key id directly in playbook, so we use now IAM Roles. Goto IAM and click on create role:
     *  select ec2 , NEXT
     *  Give full Administartor Access in policy, NEXT
     *  Role name : ansible-admin
5. now select the controller instance -> click on actions -> security -> modify IAM role : choose ansible-admin role and SAVE.


## AWS VPC and Bastion host using ansible playbooks

1. In Ansible for AWS VPC [phase 1] project we created the AWS VPC  and Bastion host, so we will use that code.
2. Now clone the repositry in the controller instance, follow the below commands. After cloning the repositry checkout to the branch vprofile-stack.
   ```console
   $ git clone https://github.com/RaviTeja110820/ansible-aws-vpc.git
   $ git branch -a       # to view where we are
   $ git checkout vprofile-stack  # to change the branch
   $ ls
   $ ls vars/
   $ rm -rf vars/output_vars
   ``` 
3. now we will start the execution
   ```console
   $ ls
   $ ansible-playbook site.yml
   $ cat vars/output_vars
   ```

## playbook to launch ec2, 

1. To get the AMI id's go to this link - https://cloud-images.ubuntu.com/locator/ec2/ . 
   > note: use which region you want the AMI while searching

2. go to my repositry and check the code there
3. we should not push the key pairs to repositry so we use .gitignore files.
   ```console
   $ vim .gitignore
           *.pem             # it will neglect the pem files
   $ git add .
   $ git commit -m "ignoring keys"
   $ git push
   ```
4. Now run ec2 stack playbook
   ```console
   $ ansible-playbook vpro-ec2-stack.yml
   $ ansible-playbook bastion-instance.yml
   $ git add .
   $ git commit -m "security grp id"
   $ git push
   ```

   > vprofile stack instances can only accessed from the bastion host. so we need to login into bastion host and frome there we can login to vprofile innstances that where in private subnet.


## Errors to resolve

```console
$ sudo apt remove ansible -y
$ sudo apt install python3-pip -y
$ sudo pip3 install ansible
$ ansible --version
```