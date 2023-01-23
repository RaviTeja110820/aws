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
Run the below commands to provision Mysql
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
   logout
   logout
   ```

## Memcache Provisioning
Run the below commands to provision Memcache
```console
$ vagrant ssh mc01
$ sudo -i
$ yum update -y
$ yum install epel-release -y
$ yum install memcached -y
$ systemctl start memcached
$ systemctl enable memcached
$ systemctl status memcached
$ memcached -p 11211 -u 11111 -u memcached -d
$ ss -tunlp | grep 11211    # to validate it running on correct port
exit
exit
```

## RabbitMQ Provisioning
Run the below commands to provision RabbitMQ
Login to the RabbitMQ vm
```console
$ vagrant ssh rmq01
```
Verify Hosts entry, if entries missing update the it with IP and hostnames
```console
$ cat /etc/hosts
```
Update OS with latest patches
```console
$ sudo -i
$ yum update -y
$ yum install wget -y
```
Set EPEL Repository
```console
$ yum install epel-release -y
```
Install Dependencies
```console
$sudo yum install wget -y
$cd /tmp/
$wget http://packages.erlang-solutions.com/erlang-solutions-2.0-1.noarch.rpm
$sudo rpm -Uvh erlang-solutions-2.0-1.noarch.rpm
$sudo yum -y install erlang socat
```
Install Rabbitmq Server
```console
$curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | sudo bash
$sudo yum install rabbitmq-server -y
```
Start & Enable RabbitMQ
```console
$sudo systemctl start rabbitmq-server
$sudo systemctl enable rabbitmq-server
$sudo systemctl status rabbitmq-server
```
Config Change
```console
$sudo sh -c 'echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config'
$sudo rabbitmqctl add_user test test
$sudo rabbitmqctl set_user_tags test administrator
Restart RabbitMQ service
$ systemctl restart rabbitmq-server
```
Enabling the firewall and allowing port 25672 to access the rabbitmq permanently
```console
$ systemctl start firewalld
$ systemctl enable firewalld
$ firewall-cmd --get-active-zones
$ firewall-cmd --zone=public --add-port=25672/tcp --permanent
$ firewall-cmd --reload
```

## TOMCAT SETUP
Login to the tomcat vm
```console
$ vagrant ssh app01
```
Verify Hosts entry, if entries missing update the it with IP and hostnames
```console
$ cat /etc/hosts
```
Update OS with latest patches
```console
$ yum update -y
```
Set Repository
```console
$ yum install epel-release -y
```
Install Dependencies
```console
$ yum install java-1.8.0-openjdk -y
$ yum install git maven wget -y
```
Change dir to /tmp
```console
$ cd /tmp/
```
Download & Tomcat Package
```console
$ wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.37/bin/apache-tomcat-8.5.37.tar.gz
$ tar xzvf apache-tomcat-8.5.37.tar.gz
```
Add tomcat user
```console
$ useradd --home-dir /usr/local/tomcat8 --shell /sbin/nologin tomcat
```
Copy data to tomcat home dir
```console
$ cp -r /tmp/apache-tomcat-8.5.37/* /usr/local/tomcat8/
```
Make tomcat user owner of tomcat home dir
```console
$ chown -R tomcat.tomcat /usr/local/tomcat8
```
Setup systemd for tomcat
Update file with following content.
```console
$ vi /etc/systemd/system/tomcat.service
[Unit]
Description=Tomcat
After=network.target
[Service]
User=tomcat
WorkingDirectory=/usr/local/tomcat8
Environment=JRE_HOME=/usr/lib/jvm/jre
Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_HOME=/usr/local/tomcat8
Environment=CATALINE_BASE=/usr/local/tomcat8
ExecStart=/usr/local/tomcat8/bin/catalina.sh run
ExecStop=/usr/local/tomcat8/bin/shutdown.sh
SyslogIdentifier=tomcat-%i
[Install]
WantedBy=multi-user.target

$ systemctl daemon-reload
$ systemctl start tomcat
$ systemctl enable tomcat
```
Enabling the firewall and allowing port 8080 to access the tomcat
```console
$ systemctl start firewalld
$ systemctl enable firewalld
$ firewall-cmd --get-active-zones
$ firewall-cmd --zone=public --add-port=8080/tcp --permanent
$ firewall-cmd --reload
```

## CODE BUILD & DEPLOY (app01)
Download Source code
```console
$ git clone -b local-setup https://github.com/devopshydclub/vprofile-project.git
```
Update configuration
```console
$ cd vprofile-project
$ vim src/main/resources/application.properties
$ Update file with backend server details
```
Build code
Run below command inside the repository (vprofile-project)
```console
$ mvn install
```
Deploy artifact
```console
$ systemctl stop tomcat
$ sleep 120
$ rm -rf /usr/local/tomcat8/webapps/ROOT*
$ cp target/vprofile-v2.war /usr/local/tomcat8/webapps/ROOT.war
$ systemctl start tomcat
$ sleep 300
$ chown tomcat.tomcat usr/local/tomcat8/webapps -R
$ systemctl restart tomcat
```
