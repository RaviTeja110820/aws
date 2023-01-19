# Ansible

Infrastructure as a code is the process of managing and provisioning computing and networking infrastructure and their configuration through machine processable definition files.

You can use interactive configuration tools to define provision and maintain your infrastructure. There are many tools such as terraform, puppet, chef, ansible etc. that can be used to achieve this.


**Ansible** is an open source automation platform that is used for configuration management, application deployment task automation etc.. It can also do IT orchestration to run tasks in sequence and create a chain of events which must happen on several different servers or devices.
> In simple terms ansible enables us to define our infrastructure as code in a simple declarative manner.

**Advantages:**
    * Ansible is an automation engine
    * An open-source platform,designed to automate IT functions
    * can easily manage complex processes and functions
    * A resource-sensitive platform
    * Realiable,poerful, and secure.


## Installation of Ansible

Ansible can be installed using Python Package Manager and Linux Repositories.

```console
sudo apt update
sudo apt install python3.7
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo apt install python3-pip
python3 -m pip install --user ansible
<!-- sudo -H pip install ansible -->
ansible --version
```

* Another method to install

```console
sudo apt-get update
apt-get install ansible
ansible --version
```

## setup

```console
sudo vim /etc/ansible/ansible.cfg  #uncomment host_key_chceking = false
```

1. To run using adhoc command
    ```console
        ansible -i inventory -m ping web1
    ```
2. to craete groups in inventory file : 
   ```console
   [websrvgrp]
    web1
    web2
    ```
3. To create groups of group in inventry file:
   ```console
    [dc_ohio:children]
    websrvgrp
    dbgrp
   ```