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