# Capstone -1
In this lab, you will create the VPC inside your AWS account. As you know, before you create VPC, you need to select a region by considering factors like cost, compliance, latency, etcetera. You will also need two subnets inside your VPC. A public subnet to host your web application. For that, you will launch an EC2 Instance. Also, a Private subnet to deploy your RDS MySQL database. Then, you will set up the connection between RDS and EC2, then install the WordPress website on the instance. Finally, you will start hosting a simple WordPress website on an EC2 instance and -> export the static assets into the S3 bucket.

![Architecture](./images/architecture.jpg)

# Steps

1. Create IAM User with console And Programatic Access.
2. Creating VPC with private and public Subnets. 
3. creating Private RDS
4. Creating EC2 and Installing Wordpress
5. Linking Database with EC2
6. Accessing the WordPress
7. export the static assets into the S3 bucket.

# Setup

## Create IAM User with console And Programatic Access.

1. Go to IAM Service In AWS Console
2. Click on Users -> Create User
3. Give the User name - WordpressUser, Enable Programmatic access and Aws Management Console Access.
   > If You are using the Root Account for the Project Setup , then You can disable the Aws Management Console Access
  ![IAM User](./images/iam-user.jpg)
4. Next: Permissions -> click on Attach Existing Policies and select **AdministratorAccess** if you want to use it for project setup , else select **S3FullAccess** .
  ![Policy](./images/policy.jpg) 
5. Review the permissions and Create user.
6. Download the CSV file and use it when you want to access AWS cli. It contains Access key id and Secret access key id.
   ![download CSV](./images/download-csv.jpg)
   

## To Create VPC with private and public Subnets:

1. Goto VPC -> Create VPC -> Give name and use 10.0.0.0/16 as IPv4 CIDR block 
   ![VPC CREATE](./images/vpc-create.jpg)

2. Create subnet -> select the vpc which  is above created
   
    * Subnet-1 -> public subnet, 10.0.0.0/24
    * Subnet-2 -> private subnet, 10.0.1.0/24
![Create subnet](./images/create-subnet.jpg)
  ![subnet-1](./images/subnet-1.jpg)
  ![subnet-2](./images/subnet-2.jpg)
1. Create InternetGateway and Attach it to vpc we created above.
   ![Internetgateway](./images/igw.jpg)
2. Create two route tables one for public and other for private. while creating select the vpc we created above.

      * select public route -> edit subnet associations -> select public subnet
      * select public route -> edit routes -> add route -> Destination - 0.0.0.0/0 , target - Internetgateway we created earlier
      * select private route -> edit subnet associations -> select private subnet
   
    ![route table](./images/route-table.jpg)


## To creat Private RDS

1. Goto RDS -> create Database
   
    * database creation method - Standard create
    * Engine type - MySQL
    * Templates - Free tier
    * DB instance identifier - database
    * Master username - admin
    * Master password - admin123
    * Disable Storage autoscaling.
    * Virtual private cloud (VPC) - Wordpress-vpc
    * Public access - **No**
    * Additional Configuration -> Database options -> Intial databse name - **wordpressdb**
    ![RDS](./images/rds.jpg)
2. After Creating Database , Select database -> click on vpc Security Group -> edit inbound rules. 
    ![RDS Security Group](./images/rds-securitygrp.jpg)

## To Creat EC2 and Installing Wordpress


![wordpress Files](./images/wordpress-files.jpg)

## To Access the WordPress

![wordpress Sigin in](./images/wordpress-sign.jpg)

![wordpress Dashboard](./images/wordpress-dashboard.jpg)

## To export the static assets into the S3 bucket.

![assets sync to s3](./images/s3-sync.jpg)

![ s3 Bucket](./images/s3-bucket.jpg)