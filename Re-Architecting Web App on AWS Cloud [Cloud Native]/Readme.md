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
3. Create Security Group for Elasticcache,RDS & ActiveMQ
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
goto keypairs and click on create new key pair:
 * name : vprofile-bean-key
 * file format : pem
 * create key pair

## Security Group
1. Security group for Backend Services:
   * name : vprofile-backend-SG
   * Description : Security group for vprofile Backend services
   * Inbound rules:
      * All Traffic,source - Backend Security Group (itself), Descripion - allow internal traffic

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
   * password : autogenarate
   * DB instance class : Burstable classes
      * db.t2.micro
   * vpc : default
   * Subnet group : vprofile-rds-sub-group
   * public access : No
   * vpc security group : vprofile-backend-SG
   * Additional Configiration -> Database options:
       * Intial database name : accounts
       * DB parameter group : vprofile-rds-para-grp
       * Option group : mysql-5-6
       * Log exports : all
   * create database  
4. copy the username , password and save some were else.