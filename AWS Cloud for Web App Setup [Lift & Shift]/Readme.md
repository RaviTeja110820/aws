# AWS Cloud for Web App Setup [Lift & Shift]

In this project users will access our website using a url and that url will be point to an Endpoint , this entry will be mentioned in Godaddy DNS . The app or browser ,use this endpoint to connect to the Loadbalancer by using https. user will access the loadbalacer using endpoint, The application load balancer will be in a security group it only allows https traffic, and then our application load balancer route the traffic to Tomcat instances . Apache tomcat instances will be running on set of instances which will be managed by autoscaling group. These Tomcat instances will be in separate security group  and only allow traffic from port 8080 only from loadbalancer. Information of backend services or backend server ip address will be mentioned in a Route 53 private DNS zone . The backend EC2 instances which will be running MYSQL, RabbitMQ and Memcache will be in a seperate security group. There is also an s3 Bucket to store the artifacts.

![Architecture](./images/architecture.jpg)


# AWS Services for this project

1. EC2 INSTANCES
2. ELB
3. AUTOSCALING
4. EFS/S3 FOR SHARED STORAGE
5. AMAZON CERTICATE MANAGE
6. ROUTE 53

# Steps
1. Login to AWS Account
2. Create Key Pairs
3. Create Security groups
4. Launch Instances with user data [BASH SCRIPTS]
5. Update IP to name mapping in route 53
6. Build Application from source code
7. Upload to S3 bucket
8. Download artifact to Tomcat Ec2 Instance
9. Setup ELB with HTTPS [Cert from Amazon Certificate Manager]
10. Map ELB Endpoint to website name in Godaddy DNS
11. Verify

# Setup

## Security Groups
1. Goto security groups and create new security group
2. Security group for Load balancer:
   * name : vprofile-ELB-SG
   * Description : Security group for vprofile prod Load Balancer
   * Inbound rules:
      * HTTP ,source - Anywhere
      * HTTPS - port 444, source- Anywhere
3. Securit group for Tomcat Instance:
   * name : vprofile-app-SG
   * Description : Security group for tomcat instances
   * Inbound rules:
      * custom TCP - port 8080 , source - Loadbalancer security group , Descripion - allow traffic from ELB
      * SSH - port 22, source - MYIP
4. Security group for Backend Services:
   * name : vprofile-backend-SG
   * Description : Security group for vprofile Backend services
   * Inbound rules:
      * MYSQL/Aurora ,source - Application security group , Descripion - allow 3306 from application servers.
      * custom tcp - port 11211 ,source - Application security group , Descripion - allows tomcat to connect memcache.
      * custom tcp - port 5672 ,source - Application security group , Descripion - allow tomcat to connect RabbitMQ. 
      * All Traffic,source - Backend Security Group, Descripion - allow internal traffic to flow on all ports.
      * SSH - port 22, source - MYIP

## Key pair
goto keypairs and click on create new key pair:
 * name : vprofile-prod-key
 * file format : pem
 * create key pair

## Launch Instance $ provision 
Go to EC2 and launch instance

1. Instance for Database mysql:
   * Name: Vprofile-mc01
   * AMI : centos7
   * Instance type : t2.micro
   * Key pair : vprofile-prod-key
   * Networking: default vpc
   * security Group: vprofile-backend-sg
   * clone the repositry https://github.com/RaviTeja110820/vprofile-project.git and go to branch aws lift and shift. Go to user data directory, copy the myql provisioning from mysql.sh file and paste in userdata and launch instance.
   *  login in and type
   ```console
   $ sudo -i 
   $ curl https://169.254.169.254/latest/userdata
   $ systemctl status mariadb
   ```
2. Instance for memcache:
   * Name: Vprofile-db01
   * AMI : centos7
   * Instance type : t2.micro
   * Key pair : vprofile-prod-key
   * Networking: default vpc
   * security Group: vprofile-backend-sg
   * clone the repositry https://github.com/RaviTeja110820/vprofile-project.git and go to branch aws lift and shift. Go to user data directory, copy the memcache provisioning from memcache.sh file and paste in userdata and launch instance.
   *  login in and type
   ```console
   $ sudo -i 
   $ curl https://169.254.169.254/latest/userdata
   $ systemctl status memcached
   ```
3. Instance for Rabbitmq:
   * Name: Vprofile-rmq01
   * AMI : centos7
   * Instance type : t2.micro
   * Key pair : vprofile-prod-key
   * Networking: default vpc
   * security Group: vprofile-backend-sg
   * clone the repositry https://github.com/RaviTeja110820/vprofile-project.git and go to branch aws lift and shift. Go to user data directory, copy the rabbitmq provisioning from rabbitmq.sh file and paste in userdata and launch instance.
   *  login in and type
   ```console
   $ sudo -i 
   $ curl https://169.254.169.254/latest/userdata
   $ systemctl status rabbitmq-server
   ```
4. Instance for Tomcat:
   * Name: Vprofile-app01
   * AMI : ubuntu18
   * Instance type : t2.micro
   * Key pair : vprofile-prod-key
   * Networking: default vpc
   * security Group: vprofile-app-sg
   * clone the repositry https://github.com/RaviTeja110820/vprofile-project.git and go to branch aws lift and shift. Go to user data directory, copy the tomcat provisioning from tomcat_ubuntu.sh file and paste in userdata and launch instance.
   *  login in and type
   ```console
   $ sudo -i 
   $ curl https://169.254.169.254/latest/userdata
   $ systemctl status rabbitmq-server
   ```
    
## Route53
1. goto Route53 and create a hosted zone:
   * Domain name : vprofile.in
   * Description: Hosted Zone for backend servers
   * Private
   * select region and default vpc
   * create 
2. Now create records:
   * select simple routing
   * define simple record : 
      * record name : db01.vprofile.in
      * endpoint : ipaddress
      * paste the private ip of db01 instance 
   * define simple record : 
      * record name : mc01.vprofile.in
      * endpoint : ipaddress
      * paste the private ip of mc01 instance 
   * define simple record : 
      * record name : rmq01.vprofile.in
      * endpoint : ipaddress
      * paste the private ip of rmq01 instance 
   * create records  

# Build 
To build the articaft you need to download jdk and maven locally on your system. Follow the bellow commands to do it
1. open powershell as administrator:
   ```console
   choco install jdk8 -y
   choco install maven -y
   choco install awscli -y
   ```
2. open the cloned repositry in git bash :
   ```console
   $ git checkout aws-LiftAndAhift
   $ cd src/
   $ cd main/
   $ cd resources/
   $ vim application.properties         # update dob01 with db01.vprofile.in same as mc01 and rmq01
   ``` 
3. now we will start the buid. go to directory were pom.xml file is there and run the below command
   ```console
   $ mvn install
   $ ls target/
   ```

# upload artifact to s3 bucket
1. create an IAM user and save the access key and secret access key password.
2.  in git bash run following commands:
   ```console
   $ aws configure
   $ aws s3 mb s3://vprofile-artifact-storage     # creats a bucket with name vprofile-artifact-storage
   $ cd vprofile-project/
   $ cd target/
   $ ls
   $ aws s3 cp vprofile-v2.war s3://vprofile-artifact-storage/
   $ aws s3 ls vprofile-artifact-storage/
   ```
# IAM Role
1. we need to give this artifact from s3 bucket to tomcat server, but we can do it automaticcaly by adding an IAM role to EC2 instance.
2. Go to IAM -> IAM role , click on create IAM role:
   * Select EC2 , Next
   * Permissions : s3 full access
   * vprofile-artifact-storage-role
   * create
3. go to Instances, select app01 instance -> Actions -> security -> modify IAM role -> select vprofile-artifact-storage-role , save
4. now application instance has the autentication to access artificat from s3bucket.

# Deploy
1. connect to the application instance.
    ```console
    $ sudo -i
    $ systemctl status tomcat8
    $ cd /var/lib/tomcat8/
    $ cd webapps/
    $ systemctl stop tomcat8
    $ rm -rf ROOT                       # default is deleted
    ```
2. Now we will install artifact from s3 Bucket
   ```console
   $ apt install awscli -y
   $ cd
   $ aws s3 ls s3://vprofile-artifact-storage
   $ aws s3 cp s3://vprofile-artifact-storage/vprofile-v2.war /tmp/vprofile-v2.war
   $ cd /tmp/
   $ ls
   $ cp vprofile-v2.war /var/lib/tomcat8/webapps/ROOT.war
   $ systemctl start tomcat8
   $ ls /var/lib/tomcat8/webapps/
   $ cd /var/lib/tomcat8/webapps/ROOT/
   $ ls
   $ cd WEN-INF/
   $ CD classes/
   $ cat application.properties         # check the changes
   ```
3. To install network connectivity
   ```console
   $ apt install telnet -y
   $ telnet db01.vprofile.in 3306
   ```

## Load Balancer
1. Go to Loadbalacer, click on target groups, create target groups:
   * Instance 
   * name : vprofile-app-TG
   * protocol - HTTP : Port -8080
   * Health check : /login
   * Advanced health settings, port -override : 8080, Healthy threshold - 3
   * select application instance , click on include as pending below
   * create target group

2. Create a loadbalncer -> Application Load balancer:
   * name: vprofile-prod-elb
   * internet facing
   * protocol- HTTPS : port- 443
   * protocol- HTTP : port- 80
   * select all Availability zones all
   * choose a certificate
   * select vprofile-elb-SG security group
   * Target group : existing target grp
      * vprofile-app-TG
      * check protocol-HTTP port-8080 and health-/login 
   * Create 