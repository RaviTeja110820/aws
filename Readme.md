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