# Multi Tier Web Application Setup Locally

In this Project we are going to setup Mutli Tier Web Application stack, the setup will be locally on Laptop/Desktop. This project Helps you to setup any project locally.

![architecture](./images/architecture.jpg)
* user can access our services from the browser by entering Ip address or an endpoint, user will be redirected to loadbalancer so we gonna setup nginx server which act like a load balancer. Nginx service is then gonna forward request to Application server. Apache tomcat will be your Application server were our java application is running. we can have a shared storage with NFS. Application server is then going to forward the request to RabbitMQ which will be our message broker and that will send the request to memcached for DataBase caching, Memcached is gonna cache the sql querys, which was exectued by mysql query server.

![Automation-arch](./images/automation-arch.jpg)

* We use Vagrant to automatically setup our virtual machine, vagrant is gonna comunicate with Oracle  vm virtual box which is the hypervisor and create virtual machine automatically on that. Then we use Bash Scripts or commannds to setup our services.

***RabbitMQ*** - Queing agent, It connects two applications together.

***Memcached Service*** - It is a database cache, it will be connected to mysql server.

***NGINX*** - It is an opensource software for web serving,reverse proxing,caching,load balancing,media straming etc.


# Tools
1. HYPERVISOR - ORACLE VM VIRTUALBOX
2. AUTOMATION - VAGRANT
3. CLI - GIT BASH
4. IDE - SUBLIME TEXT
   
# Steps
1. Clone source code
2. cd into vagrant directory
3. Bring up vm's
4. Setup All services
   * Mysql
   * Memcached
   * Rabbit MQ
   * Tomcat
   * Nginx

# Setup

1. clone the project into your Drive using the below command in cmd or git bash
   ```console
   $ git clone https://github.com/RaviTeja110820/vprofile-project.git
   ```
2. now execute the below commands:
   ```console
   $ ls
   $ cd vprofile-project/
   $ ls
   $ git checkout local-setup
   $ cd vagrant/
   $ cd Manual_provisioning/
   $ ls
   $ cat Vagrantfile       # to view
   ```

3. to execute follow below comands:
   ```console
   $ vagrant up
   ```
4. By running previous command , all the vms are created, to verify follow below commands:
   ```console
   $ vagrant ssh web01        # you will goto the web01 machine
   $ cat /etc/hosts           
   $ ping app01               # to check if it is connected to other machines
   $ logout                   # to exit from web01
   ```

## Mysql Provisioning
1. Run the below commands to provision Mysql
   ```console
   $ vagrant ssh db01
   $ sudo -i                            # switching to root user
   $ yum update -y                      # to update
   $ DATABASE_PASS='admin123'           # variable to save password,but it is temporary
   $ vi /etc/profile                    # now write the DATABASE_PASS='admin123' in this , it will be permenant now.
   $ source /etc/profile 
   $ yum install epel-release -y
   $ yum install git mariadb-server -y  # For centos we use mariadb serverand for ubuntu we use mysql
   $ systemctl start mariadb
   $ systemctl enable mariadb
   $ systemctl status mariadb
   $ mysql_secure_installation          # it asks to set password give password as  - admin123
   $ mysql -u root -p
   exit
   $ git clone https://github.com/RaviTeja110820/vprofile-project.git
   $ cd vprofile-project/
   $ cd main/
   $ cd resources/
   $ pwd
   $ mysql -u root -p"DATABASE_PASS" -e "create database accounts"
   $ mysql -u root -p"DATABASE_PASS" -e "grant all privileges on accounts.* TO 'admin'@'app01' identified by 'admin123'" # we gave app01 admin access for database
   $ cd ../../..                 # we need to go to vprofile-project directory
   $ mysql -u root -p"$DATABASE_PASS" accounts < src/main/resources/db_backup.sql
   $ mysql -u root -p"$DATABASE_PASS" -e "FLUSH PRIVILEGES"
   $ mysql -u root -p"$DATABASE_PASS"
   show databases;
   use accounts;
   show tables;
   exit
   ```