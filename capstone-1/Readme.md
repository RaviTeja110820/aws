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

![VPC](./images/vpc.jpg)

## To creat Private RDS

![RDS](./images/rds.jpg)

![RDS Security Group](./images/rds-securitygrp.jpg)

## To Creat EC2 and Installing Wordpress


![wordpress Files](./images/wordpress-files.jpg)

## To Access the WordPress

![wordpress Sigin in](./images/wordpress-sign.jpg)

![wordpress Dashboard](./images/wordpress-dashboard.jpg)

## To export the static assets into the S3 bucket.

![assets sync to s3](./images/s3-sync.jpg)

![ s3 Bucket](./images/s3-bucket.jpg)