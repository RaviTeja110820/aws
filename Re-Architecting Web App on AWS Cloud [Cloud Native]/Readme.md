# Re-Architecting Web App on AWS Cloud [Cloud Native]

![Architecture](./images/architecture.jpg)

# AWS Services

1. BEANSTALK        - VM FOR TOMCAT, NGINX LB REPLACEMENT, AUTOMATION FOR VM SCALING
2. S3/EFS           - STORAGE
3. RDS INSTANCE     - DATABASES
4. ELASTIC CACHE    - MEMCACHED
5. ACTIVE MQ        - RABBIT MQ
6. ROUTE53          - DNS
7. CLOUDFRONT       - CONTENT DELIVERY NETWORK

# Steps

1. Login to aws account
2. Create Key pair for beanstalk instance login
3. Create Security Group for Elasticache,RDS & ActiveMQ
4. Create
   * RDS
   * Amazon Elastic Cache
   * Amazon Active MQ
5. Create Elastic Beanstalk Environment
6. Update SG of backend to allow traffic from Bean SG
7. Update SG of backend to allow internal traffic
8. Update Entry in GoDaddy DNS Zones

# Setup

## Key pair

goto key pairs and click on create new key pair:

* name : vprofile-bean-key
* file format : pem
* create key pair

## Security Group

1. Security group for Backend Services:
   * name : vprofile-backend-SG
   * Description : Security group for vprofile Backend services
   * Inbound rules:
      * All Traffic,source - Backend Security Group (itself), Description - allow internal traffic
      * MYSQL/Aurora ,source -  security group of instance(mysql-sg) , Description - allow 3306 from instance servers.
2. Security group for instance
   * name : mysql-sg
   * Inbound rules:
     * SSH , port - 22 : MYIP  

## RDS

1. Select subnet Groups -> Create DB subnet group:
   * Name : vprofile-rds-sub-group
   * Description : vprofile-rds-sub-group
   * Availability zones : all
   * subnets : all
2. Click on Parameters groups -> create parameter group:
   * parameter group family : mysql5.6
   * Group name : vprofile-rds-para-grp
   * Description : vprofile-rds-para-grp

3. Click Databases -> Create database:
   * creation mode : Standard create
   * Engine : MySQL
   * version : MySQL 5.6.34
   * Template : Dev/Test
   * DB instance identifier : vprofile-rds-mysql
   * Master username : admin
   * password : autogenerate
   * DB instance class : Burstable classes
      * db.t2.micro
   * vpc : default
   * Subnet group : vprofile-rds-sub-group
   * public access : No
   * vpc security group : vprofile-backend-SG
   * Additional Configuration -> Database options:
       * Initial database name : accounts
       * DB parameter group : vprofile-rds-para-grp
       * Option group : mysql-5-6
       * Log exports : all
   * create database  
4. copy the username , password and save some were else.
![RDS](./images/RDS.jpg)

## ElastiCache

1. open ElastiCache in aws console
2. click on parameters group -> create parameters group:
   * family: memcached 1.4
   * Name: vprofile-memcached-para-grp
   * Description: vprofile-memcached-para-grp
3. click on subnet groups -> create subnet groups:
   * Name: vprofile-memcached-sub-grp
   * Description: vprofile-memcached-sub-grp
   * VPC - default
   * select all zones, subnets and add them.
   * create
4. Click on memcached -> create:
   * cluster engine : Memcached
   * Name : vprofile-elasticache-svc
   * Engine version : 1.4.5
   * port : 11211
   * parameter grp : vprofile-memcached-para-grp
   * Node type : cache-t2.micro
   * number of nodes : 1
   * Advanced memCached settings:
     * subnet group : vprofile-memcached-sub-grp
     * security group : vprofile-backend-SG
     * create  
![elastic cache](./images/elasticache.jpg)

## Amazon MQ

1. Goto Amazon MQ in aws console
2. click on Get started:
   * Deployment mode : single instance
   * storage type : Durability optimized
   * Next
   * Broker name : vprofile-rmq
   * instance type : mq.t2.micro
   * ActiveMQ Access :
     * chose simple Authentication and Authentication
     * Username  : Rabbit
     * Password :  blue7890bunny
   * Additional Settings:
     * logs -> cloudwatch logs:
       * choose General and Audit
     * Security group : vprofile-backend-SG
     * Public accessibility : No
   * create broker  
![RabbitMQ](./images/rabbitmq.jpg)

## Database initializing

1. Goto EC2 and click on launch Instance:
   * Name: mysql-client
   * AMI : Ubuntu 18
   * Instance type : t2.micro
   * key pair - vprofile-bean-key  
   * VPC - default
   * Security group : mysql-sg
2. connect to the instance mysql-client

   ```console
   ssh -i Downloads/vprofile-bean-key.pem ubuntu@InstanceIP
   ```

3. Run the below commands in the instance to link the database:

   ```console
   sudo apt update            # to update the instance
   sudo yum install mysql-server
   mysql -h <RDS_Endpoint_Link> -P 3306 -u <username> -p
   git clone https://github.com/devopshydclub/vprofile-project.git
   cd vprofile-project/
   git branch -a
   git checkout aws-Refactor
   ```

4. To initialize the database follow the commands:

   ```console
   cd src/main/resources/
   mysql -h <RDS_Endpoint_Link> -P 3306 -u <username> -p<password> accounts  < db_backup.sql
   mysql -h <RDS_Endpoint_Link> -P 3306 -u <username> -p<password> accounts
   ```

5. Database initialize is done , Now Terminate the mysql-client instance.

## Elastic Bean Stalk

1. Go to elastic bean stalk and click on create Application:
   * Application name: vprofile
   * Platform : Tomcat
   * Application code : Sample Application
   * click on configure more options :
     * select Instances:
       * Add vprofile-backend-SG security group
       * Root volume type: General purpose(SSD)
       * size : 8GB
       * save
     * select capacity :
       * Environment type : Load balanced
       * instances : Min-2 and Max-8
       * instance type : t2.micro
       * save
     * select Load balancer :
       * Application load balancer
       * save
     * select modify rolling updates and deployments:
       * Deployment policy : Rolling
       * Batch size : 50%
       * save
     * select security :
       * EC2 key pair : vprofile-bean-key
       * save
     * select Modify monitoring:
       * log streaming : Enable
       * Lifecycle : Delete Logs upon termination
     * select Tags:
       * Project : vprofile-app
   * click on Create app

2. After some time copy the url provided and paste in new tab, if you see congratulations then its ok.
   ![Health ok](./images/healthok.jpg)

3. In backend security group add :
   * mysql/Aurora : security group of elastic bean stalk
   * custom TCP , port: 11211 : security group of elastic bean stalk
   * custom TCP , port: 5671 : security group of elastic bean stalk

4. go to elastic bean stalk -> environments -> configuration:
   * Edit load balancer:
     * Add listener -> port :443 , protocol : HTTPS , choose SSL certificate and add.
     * process -> Actions -> edit : port - 80, path - /login and save
     * Now Apply all the changes
5. we haven't uploaded our artifact so health appears as severe so do not worry.

## Build and Deploy Artifact

1. open git bash and clone the repository - <https://github.com/devopshydclub/vprofile-project.git>
2. follow the below commands:

     ```console
   cd vprofile-project/
   git branch -a
   git checkout aws-Refactor
   ```

3. now we will change the application properties file:

   ```console
   $ cd src/main/resources/
   $ vim application.properties         # add RDS , Memcached , RabbitMq endpoint links and change the password of what you entered while $ $ creating RDS
   $ cd ../../..                        # go to vprofile project directory 
   ```

4. Lets build

   ```console
   mvn install                # Build Success
   ls target/                 # you can see the war file created
   ```

5. Go to elastic beanstalk -> Application versions -> click on upload
   * version label : vprofile-V2.5
   * choose file : choose the war file you generated
   * upload

6. now select the version you have uploaded and click on actions -> Deploy

7. if the health is in OK copy the endpoint link and paste in new tab, you can see the sign in page.
   ![login](./images/login.jpg)

## DNS

1. Goto DNS of your Domain Name
2. Add a record:
   * type: CNAME
   * Host : vprofile
   * points to : Endpoint link of elastic bean stalk
   * save

3. wait for some time and go to new tab and type - <https://vprofile.groophy.in>
4. to login username and password is admin_vp


## Amazon CloudFront

1. create Distribution :
   * Origin Domain Name : vprofile.groophy.in
   * Origin protocol policy : match viewer
   * protocol policy : HTTP and HTTPS
   * HTTPS methods : ALL
   * Distribution Settings : 
     * Alternate Domain Name(CNAME) : vprofile.groophy.in
     * SSL certificate : custom SSL certificate, choose your certificate
     * security policy : TLSv1
   * submit

2. once the status is changed from in progress to Deployed, now <https://vprofile.groophy.in/login>