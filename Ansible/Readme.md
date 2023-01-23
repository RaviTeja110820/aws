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
$ sudo vim /etc/ansible/ansible.cfg  #uncomment host_key_chceking = false
```

1. To run host using adhoc command
    ```console
       $ ansible -i inventory -m ping web1          # to run single host
       $ ansible -i inventory -m ping web2
       $ ansible -i inventory -m ping all           # to run all hosts in inventory file
       $ ansible -i inventory -m ping web1 '*'      # to run all hosts in inventory file

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

4. Variables at group level in inventory file
   ```console
   [webservgrp:vars]
   ansible_users=centos
   ansible_ssh_private_key_file=virginia_key.pem
   ```

## adhoc commands

```console
$ ansible -i inventory -m yum -a "name=httpd state=present" web1 --become      #it installs the httpd using yum on web1 server , --become makes web1 into root to execute the command. -a -> arguments, -m -> module
```

```coonsole
$ ansible -i inventory -m service -a "name=httpd state=started enabled=yes" web1 --become
```

```console
$ ansible -i inventory -m copy -a "src=index.html dest=/var/www/html/index.html" web1 --become
```
```console
$  ansible -i inventory  -m yum -a "name=httpd state=absent" web1 --become       # to delete the httpd 
```

## Playbooks

Playbooks are written in YAML format
> YAML - Yet Another Markup language
```yaml
---
- name: Setup WebServer                     # play
  hosts: websrvgrp
  become: yes
  tasks:
    - name: Install Apache httpd 
      yum:
         name: httpd
         state: present
    - name: Start & Enable HTTPD
      service:
        name: httpd
        state: started
        enabled: yes

    - name: Copy index file
      copy:
        src: index.html
        dest: /var/www/html/index.html

- name: Setup DBserver                      # play
  hosts: dbsrvgrp
  become: yes
  tasks:
    - name: Install MySQL server
      yum:
         name: mariadb-server
         state: present
    - name: Start & Enable maridb service
      service:
         name: mariadb
         state: started
         enabled: yes

```

```console
$ ansible-playbook -i inventory web_db.yaml --syntax-check    # to check the synatx is correct or not, it return the file name if everything is perfect
```console
$ ansible-playbook -i inventory web_db.yaml     # to run the playbook
```

```console
$ ansible-doc -l         # it will list all the modules

$ ansible-doc yum        # to see about yum module
```

## Order of Ansible config
1. ANSIBLE_CONFIG (environment variable if set)
2. ansible.cfg (in the current directory)
3. ~/.ansible.cfg (in the home directory)
4. /etc/ansible/ansible.cfg
