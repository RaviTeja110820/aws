# Wordpress using Elastic BeanStalk

AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, and Docker on familiar servers such as Apache HTTP Server, Apache Tomcat, Nginx, Passenger, and IIS. You can simply upload your code and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring.


  I Deploy an Elastic Beanstalk to host my website on wordpress. first we need create all the dependencies such as VPC, subnet, Internetgateway, Roting  tables. A wordpress website needs a database to work, which means we will need to create an RDS and Creation of the Beanstalk. We also need an Elastic Load Balancer. Those resources wil need to be on a multiple Availability Zones.
# Steps

# Setup