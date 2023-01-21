# Ansible for AWS VPC

In this project we are going to use ansible to automate aws vpc setup and also baston host. 
> make sure you use a region that has minimum 3 availability zones like ohio

![Architecture](./images/architecture.jpg)

# Flow of Execution

* Login to AWS
* Create ec2 instance to run ansible playbok
* Install Ansible
* Install boto
* Setup ec2 Role for ansible
* Create a project directory
* Sample cloud task (with key pair)
* Create Variables File for VPC & Baston host
* Create VPC Setup Playbook
* Create Baston setup playbook
* Site.yml playbook to call both playbook at once

# setup
1. sign in to aws console and click on launch instance:
    * name : control-machine
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
3. Dont put access key and secret access key id directly in playbook, so we use now IAM Roles. Goto IAM and click on create role:
     *  select ec2 , NEXT
     *  Give full Administartor Access in policy, NEXT
     *  Role name : ansible-admin
4. now select the control-machine instance -> click on actions -> security -> modify IAM role : choose ansible-admin role and SAVE
5. Now check if the permissions is added or not.  Connect to contrl-machine instance and run below commands:
    ```console
    $ sudo apt install awscli -y
    $ aws sts get-caller-identity   # it will return the what role it used.
    ```
## Sample cloud task
1. first create a project directory in the control-machine instance by running below command:
   ```console
   $ mkdir vpc-stack-vprofile
   $ cd vpc-stack-vprofile
   ```

2. goto **ansible module index documentation**, and navigate to cloud modules, there you can see lot of aws modules. For now select ec2_key-create or delete an ec2 key pair. go to examples. now run the below commands in control-machine instance.
   ```console
   $ vim test-aws.yml
   ```
* now type the below yaml code in test-aws.yml file
    ```yaml
    - hosts: localhost
      connection: local
      gather_facts: False
      tasks:
        - name: sample ec2 key
          ec2_key:
            name: sample
            region: us-east-2
          register: keyout
        - debug:
            var: keyout
        - name: store login key
          copy:
            content: "{{keyout.key.private_key}}"
            dest: ./sample-key.pem
          when: keyout.changed
    ```
* to execute the playbook run the below command:
    ```console
    $ ansible-playbook test-aws.yml
    ```
* You will get error, because we havent installed boto3. Run the below command to install boto3
    ```console
    $ sudo apt search boto  # after running this command you will get some boto installation commands, try one after other and execute above playbook, like below command
    $ sudo apt install python3-boto3 -y
    ```
* after executing the above playbook -> go to aws console -> goto key pairs, and you can see sample keypair created.
  
* now we delete the keypairs and test-aws.yml file also.
  ```console
  $ ls
  $ rm -rf *
  $ ls
  ```

## Github

1. create a repositry
2. name : ansible-aws-vpc , public
3. add a README file

## Create Variables File for VPC & Baston host
1. the variables files for both vpc and Baston host is to be uploaded to the created repositry. file names are: bastion_setup and vpc_setup
  repositry link - https://github.com/RaviTeja110820/ansible-aws-vpc

2. Now clone the repositry in control-machine instance. in the directory vpc-stack-vprofile. follow the below comand.
   ```console
   $ git clone  https://github.com/RaviTeja110820/ansible-aws-vpc
   ```
   ```console
   $ ls
   $ cd ansible-aws-vpc/
   $ ls
   ```
## Create VPC Setup Playbook
1. pull the changes and execute the command
   ```console
   $ cd ansible-aws-vpc/
   $ git pull
   $ ansible-playbook vpc-setup.yml
   ```
2. if above exection is success , then go and check in your aws console -> goto vpc. see if the vpc is created or not.
3. Run the below command to check saved id's:
   ```console
   $ ls
   $ cat vars/output_vars
   $ ls
   $ git add. 
   $ git config --global user.name xyz
   $ git config --global user.email xyz@gmail.com
   $ git commit -m "vars output"
   $ git push
   ```

## Create Baston setup playbook
1. now copy the private key of bastion and save to your local computer and connect to bastion host using the private key 
 
 ```console
 $ cat bastion-key.pem
 ```
2. connect to bastion instance
   ```console
   $ ssh -i Downloads/bastion-key.pem ec2-user@IP-address
   ```