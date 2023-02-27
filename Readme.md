# Devops

**Devops** - Devops is a culture that improves the Delivery of the organization.

Devops is a process of improving Delivery by ensuring that there is  a proper automation with a code quality that is maintained and ensuring that there is continuos monitoring and continuos testing in place.

## Why Devops

![Why Devops](./images/whydevops.jpg)

## Software Development Life Cycle (SDLC)

it is a set of standard that is followed in the software industry to Design,Develop and test. The end goal is to deliver a high quality product. 

## Linux

* Kernel has four primary Responsibilities:
  * Device Management
  * Memory Management
  * Process Management
  * Handling system calls

## Configuration Management 

There are several configuration management tools : Chef, Puppet, Ansible and salt

| Puppet | Ansible |
| --- | ----------- |
| pull model | push model |
| master/slave Architecture | Agentless Architecture |
| puppet language | simple yaml |

> using Ansible Galaxy modules can be shared

### Ansible

> Ansible supports linux (ssh) and windows (win RM). Ansible uses python programming language. using python we can create modules.

1. To install ansible run below commands on ansible server :

   ```console
   $ sudo apt update           # to update packages
   $ sudo apt install ansible  # to install ansible
   $ ansible --version         # to check the version of ansible
   ```

2. To login to target system without password:

   ```console
   $ ssh-keygen               # it will create a public key and private key
   $ ls /home/ubuntu/.ssh/    # location of keys created
   $ cat /home/ubuntu/.ssh/id_rsa.pub       # viewing the public key, copy it
   ```

   Now login to the target system and run below commands

   ```console
   $ ssh-keygen                  # it will create a public key and private key
   $ ls ~/.ssh/                  # keys location
   $ vim ~/.ssh/authorized_keys  # paste the copied content of public key from ansible system and save the files (ESC -> :x)
   ```

   Now login back to Ansible system

   ```console
   $ ssh 172.31.62.28     # mention private ip of target system to login to target system without password or key
   ```

3. lets run some adhoc commands. first create an inventory file in Ansible server and store private ip of target system in it.

   ```console
   $ vim inventory        # enter the private ip of target system
   $ ansible -i inventory all -m "shell" -a "touch devopsclass"   # it creates a file with name devopsclass in the target system.
   ```

   > To checkout more modules, goto Ansible documentation and search for ansible modules.

   > ansible adhoc is for to execute one or two tasks and ansible playbook is for multiple tasks to execute

4. if you have multiple target systems then you need to enter their private ips in inventory by grouping.

   ```vim
   [dbservers]
   172.31.62.28

   [webservers]
   172.31.62.10
   ```

   To execute the playbook for a specific group then:

   ```console
   $ ansible -i inventory webservers -m "shell" -a "touch devopsclass"   # command will be executed in systems under webservers group in inventory.
   ```

5. lets write the ansible playbook to Install Nginx and restart Nginx:

   ```console
   $ vim first-playbook.yml
   ```

   ```yml
   ---
   - name: Install Nginx
     hosts: all
     become: true
     tasks:
       - name: Install Nginx
         apt:
           name: nginx
           state: present
       - name: Start Nginx
         service:
           name: nginx
           state: started
   ```

   To execute the above playbook run the below command

   ```console
   $ ansible-playbook -i inventory first-playbook.yml
   $ ansible-playbook -vvv -i inventory first-playbook.yml   # v -> verbosity (debugging)
   ```

6. Ansible Roles is efficient way of writing ansible playbooks that will only improve your efficiency to write complex playbooks.

   ```console
   $ mkdir second-playbook
   $ cd second-playbook/
   $ ansible-galaxy role init kubernetes
   $ ls
   $ ls kubernetes/
   ```

## Infrastructure as a code

Infrastructure as code (IaC) is a software development practice that involves defining and provisioning infrastructure resources, such as servers, storage, and networking, in a declarative configuration language. This approach treats infrastructure as if it were software, and uses code to manage infrastructure resources in a more efficient and consistent manner.

### Terraform

Terraform is an open-source infrastructure as code (IaC) tool that enables developers to define and provision infrastructure resources such as servers, storage, networking, and application services in a declarative configuration language. It was created by HashiCorp and supports multiple cloud providers, including Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform (GCP), and many others.

API(Application Programming Interfaces) as code is based on the principles of Infrastructure as code (IaC) and is often used in conjunction with IaC tools like Terraform, Ansible, and Chef to automate the creation and management of API infrastructure resources like servers, networking, and security.

1. Go to browser and search  for hashicorp terraform aws.
2. To install terraform goto this link and choose your os <https://developer.hashicorp.com/terraform/downloads>
3. to check terraform is installed or not:

   ```console
   $ terraform -version
   ```

4. if you are using aws provider than configure the aws cli :

   ```console
   $ aws configure
   ```

5. lets first write main.tf file which contains all the requirements

   ```console
   $ vim main.tf
   ```

   Goto this terraform documentation <https://registry.terraform.io/providers/hashicorp/aws/latest/docs>

   ```tf
   terraform {
      required_providers {
         aws = {
            source  = "hashicorp/aws"
            version = "~> 4.16"
         }
      }

      required_version = ">= 1.2.0"
   }

   provider "aws" {
      region  = "us-west-2"
   }

   resource "aws_instance" "app_server" {
      ami           = "ami-830c94e3"
      instance_type = "t2.micro"

      tags = {
         Name = "Terraform_Demo"
      }
   }

   ```

6. Terraform runs on four commands:

   ```console
   $ terraform init     # it initializes terraform
   $ terraform plan     # it shows what the terraform going to do
   $ terraform apply    # it will apply the changes
   $ terraform destroy  # to destroy everything 
   ```

7. The outputs.tf file gives the outputs you needed after terraform apply like public and private ip details.

   ```console
   $ vim outputs.tf
   ```

8. Using terraform.tfstate file the terraform can track the changes in infrastructure. Never store the state file in source control . you should store state files remotely. Do not manipulate the state file.

![terraform](./images/terraform.jpg)

## Jenkins

jenkins is a java based Application

### Install Jenkins.

Pre-Requisites:
 - Java (JDK)

### Run the below commands to install Java and Jenkins

Install Java

```console
sudo apt update
sudo apt install openjdk-11-jre
```

Verify Java is Installed

```console
java -version
```

Now, you can proceed with installing Jenkins

```console
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

**Note:** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

* EC2 > Instances > Click on Instance-ID
* In the bottom tabs -> Click on Security
* Security groups
* Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed `All traffic`.

### Login to Jenkins using the below URL:

<http://<ec2-instance-public-ip-address>:8080>    [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing `All Traffic` to your EC2 instance
      1. Delete the inbound traffic rule for your instance
      2. Edit the inbound traffic rule to only allow custom TCP port `8080`
  
After you login to Jenkins, 
      - Run the command to copy the Jenkins Admin Password - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
      - Enter the Administrator password

Click on Install suggested plugins

## Install the Docker Pipeline plugin in Jenkins:

* Log in to Jenkins.
* Go to Manage Jenkins > Manage Plugins.
* In the Available tab, search for "Docker Pipeline".
* Select the plugin and click the Install button.
* Restart Jenkins after the plugin is installed.

## Docker Slave Configuration

Run the below command to Install Docker

```console
sudo apt update
sudo apt install docker.io
```

### Grant Jenkins user and Ubuntu user permission to docker deamon.

```console
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

Once you are done with the above steps, it is better to restart Jenkins. `<http://<ec2-instance-public-ip>:8080/restart>`

The docker agent configuration is now successful.


## Tasks

### ssh key generation

1. type below command to check ssh is installed or not
  
   ```console
   $ which ssh
   ```

2. now run below commands:

   ```console
   $ sudo -i        # goto root user
   $ java -version
   $ apt install ssh
   $ /etc/init.d/ssh start     # enable the ssh
   ```

3. lets create a user:

   ```console
   $ useradd -m -d /home/jenkins jenkins
   $ su jenkins
   $ whoami
   $ ssh-keygen
   $ ls ~/.ssh/     # we have public and private key
   ```

4. to create authorized keys 

   ```console
   $ su jenkins
   $ cd .ssh
   $ ls
   $ cat id_rsa.pub
   $ cat id_rsa.pub > authorized_keys
   $ ls
   ```

5. to send to remote server form host:

   ```console
   $ ssh-copy-id [user@]hostname
   ```

6. in remote server

   ```console
   $ sudo chown ubuntu:ubuntu /var/www
   $ sudo chmod 755 /var/www
   $ /etc/ssh/sshd_config    # password authentication yes
   ```
