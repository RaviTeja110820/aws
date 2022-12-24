***AWS GuardDuty*** is a service that provides intelligent threat detection for your AWS infrastructure and resources. AWS GuardDuty identifies threats by continually monitoring the network activity and account behavior within your AWS environment.

***AWS Shield*** is a service that helps protect your applications against distributed denial-of-service (DDoS) attacks .

***Amazon Inspector*** is a service that checks applications for security vulnerabilities and deviations from security best practices.

>A service that lets you monitor network requests that come into your web applications - ***AWS WAF***.



# Cloud Trail
With ***CloudTrail***, you can view a complete history of user activity and API calls for your applications and resources.  Events are typically updated in CloudTrail within 15 minutes after an API call was made. You can filter events by specifying the time and date that an API call occurred, the user who requested the action, the type of resource that was involved in the API call, and more.

***AWS CloudTrail*** is a service that primarily tracks governance, compliance, operational auditing, and risk auditing of your AWS account. CloudTrail logs continuously monitors, and retains account activity related to actions across all AWS infrastructure. CloudTrail provides event history of AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and troubleshooting.

# AWS CloudWatch 
***Amazon CloudWatch*** is a service that provides data that you can use to monitor your applications, optimize resource utilization, and respond to system-wide performance changes.

An alarm in ***AWS CloudWatch*** that triggers after exceeding the bill will not meet the requirements of staying within the desired budget. The alarm triggers when the account billing exceeds the threshold specified. It triggers only when actual billing exceeds the threshold.
# AWS Trusted Advisor
***AWS Trusted Advisor*** is an online tool that inspects your AWS environment and provides real-time guidance in accordance with AWS best practices.

>*Enterprise and Business* Support plans include access to all AWS Trusted Advisor checks. The *Basic and Developer* Support plans provide access to a limited selection of AWS Trusted Advisor checks.

***AWS Trusted Advisor*** also helps improve the performance of your services by providing recommendations for how to take advantage of provisioned throughput.

>Trusted Advisor provide best practices and/or or checks on *Cost Optimization, Performance, Security, and Fault Tolerance.*
# Global Infrastructure
***Availability Zone*** is a single data center or a group of data centers within a Region.  Availability Zones are located tens of miles apart from each other. This helps them to provide interconnectivity to support the services and applications that run within a Region.
>There are at least *3 Availability Zones* per AWS Region. Some regions may contain more.

>A separate geographical location with multiple locations that are isolated from each other  ***Region.***

>The server from which Amazon CloudFront gets your files  ***origin***.

>A site that Amazon CloudFront uses to cache copies of content for faster delivery to users at any location  ***Edge location***.
A *Distribution* is made up of Edge Locations that you want to serve content from, and details about how that content will be tracked an managed.

***Amazon CloudFront*** is a content delivery service. It uses a network of edge locations to cache content and deliver content to customers all over the world. When content is cached, it is stored locally as a copy. This content might be video files, photos, webpages, and so on.

>There are at least 3 Availability Zones per AWS Region. Some regions may contain more.
# Plans
The ***AWS Free Tier*** is not a Support plan. It is a program that consists of three types of offers that allow customers to use AWS services without incurring costs: Always free, 12 months free, and Trials.

***Amazon Route 53*** is a DNS web service. It gives developers and businesses a reliable way to route end users to internet applications that are hosted in AWS. Additionally, you can transfer DNS records for existing domain names that are currently managed by other domain registrars, or register new domain names directly within Amazon Route 53.

>***AWS Artifact*** is a service that enables you to access AWS security and compliance reports and special online agreements.
***AWS Artifact*** is a comprehensive resource center for access to AWS’ auditor issued reports as well as security and compliance documentation from several renowned independent standards organisations.

>Automate the deployment of workloads into your AWS environment  ***AWS Quick Starts***.

***Refactoring*** is migration strategy involves changing how an application is architected and developed, typically by using cloud-native features.

***Repurchasing*** involves replacing an existing application with a cloud-based version, such as software found in AWS Marketplace.

**Rehosting** involves moving an application to the cloud with little to no modifications to the application itself. It is also known as “lift and shift.”

***Replatforming*** involves selectively optimizing aspects of an application to achieve benefits in the cloud without changing the core architecture of the application. It is also known as “lift, tinker, and shift.”

# S3
In the ***S3 Intelligent-Tiering*** storage class, Amazon S3 monitors objects’ access patterns. If you haven’t accessed an object for 30 consecutive days, Amazon S3 automatically moves it to the infrequent access tier, S3 Standard-IA. If you access an object in the infrequent access tier, Amazon S3 automatically moves it to the frequent access tier, S3 Standard.

>Data is organised in S3 into **Archives**, and **Vaults** are used to group Archives together. **Access policies** control who can access the data in Archives & Vaults.

***S3 Glacier*** is a low-cost storage class that is ideal for data archiving. You can retrieve objects stored in the S3 Glacier storage class within a few minutes to a few hours.

The ***S3 Standard-IA*** storage class is ideal for data that is infrequently accessed but requires high availability when needed. Both S3 Standard and S3 Standard-IA store data in a minimum of three Availability Zones. S3 Standard-IA provides the same level of availability as S3 Standard but at a lower storage price. 

***S3 One Zone-IA*** is ideal for infrequently accessed data that does not require high availability.

***Amazon Simple Storage Service (Amazon S3)*** is a service that provides object-level storage. Amazon S3 stores data as objects within buckets.
>*Amazon S3 buckets* cannot be attached to Amazon EC2 instances.

In the ***S3 Intelligent-Tiering*** storage class, Amazon S3 monitors objects’ access patterns. If you haven’t accessed an object for 30 consecutive days, Amazon S3 automatically moves it to the infrequent access tier, S3 Standard-IA. If you access an object in the infrequent access tier, Amazon S3 automatically moves it to the frequent access tier, S3 Standard.

>***Access Control Lists*** let you control access to individual objects within an S3 bucket, where as ***Bucket Policies*** allow you to control access to entire buckets. In relation to S3.

>AWS has updated the URL format for objects in S3 in order to partition the name space. This will introduce more consistency, but be aware that there are still multiple variation depending on feature and location. - *https, then the bucket name, then dot, then the AWS S3 regional endpoint, then slash, then the object name.*

**S3 Intelligent-Tiering** is the first cloud object storage class that delivers automatic cost savings by moving data between two access tiers — frequent access and infrequent access — when access patterns change, and is ideal for data with unknown or changing access patterns.S3 Intelligent-Tiering stores objects in two access tiers: one tier that is optimized for frequent access and another lower-cost tier that is optimized for infrequent access. For a small monthly monitoring and automation fee per object, S3 Intelligent-Tiering monitors access patterns and moves objects that have not been accessed for 30 consecutive days to the infrequent access tier. There are no retrieval fees in S3 Intelligent-Tiering. If an object in the infrequent access tier is accessed later, it is automatically moved back to the frequent access tier. No additional tiering fees apply when objects are moved between access tiers within the S3 Intelligent-Tiering storage class. S3 Intelligent-Tiering is designed for 99.9% availability and 99.999999999% durability, and offers the same low latency and high throughput performance of S3 Standard.

>**Amazon S3 Transfer Acceleration** enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront’s globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.
# 
You upload your application, and ***Elastic Beanstalk*** automatically handles the deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring.

>***AWS Outposts*** is a service that enables you to run infrastructure in a hybrid cloud approach.

>***AWS Snowball*** is a device that enables you to transfer large amounts of data into and out of AWS.



# Well Architected Frame Work
The ***Performance Efficiency pillar*** focuses on using computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.

The ***Operational Excellence pillar*** includes the ability to run workloads effectively, gain insights into their operations, and continuously improve supporting processes to deliver business value. 

The ***Security pillar*** focuses on protecting data, systems, and assets. It also focuses on using cloud technologies to improve the security of your workloads.

The ***Reliability pillar*** focuses on the ability of a workload to consistently and correctly perform its intended functions.

# AWS Organizations
In ***AWS Organizations***, you can centrally control permissions for the accounts in your organization by using service control policies (SCPs). Additionally, you can use the consolidated billing feature in AWS Organizations to combine usage and receive a single bill for multiple AWS accounts.

***AWS Organizations*** allows the user to automate the creation of new AWS accounts when they need to quickly launch new workloads. The administrator can add these new accounts to user-defined groups in an organization for easy categorization. For example, you can create separate groups to categorize development and production accounts, and then apply a Service Control Policy (SCP) to the production group allowing only access to AWS services required by production workloads.

#
***AWS Identity and Access Management (IAM)*** is a service that you can use to manage access to AWS services and resources. 

>***AWS Key Management Service (AWS KMS)*** enables you to create, manage, and use cryptographic keys.

# Networking
A virtual private gateway enables you to establish a virtual private network (VPN) connection between your VPC and a private network, such as an on-premises data center or internal corporate network.
> A *virtual private gateway* allows traffic into the VPC only if it is coming from an approved network.

An ***internet gateway*** is a connection between a VPC and the internet. It allows public traffic from the internet to access a VPC.

A ***subnet*** is a section of a VPC in which you can group resources based on security or operational needs.

Provision an isolated section of the AWS Cloud to launch resources in a virtual network that you define  ***Amazon Virtual Private Cloud (Amazon VPC)***.

>A *network access control list (ACL)* is a virtual firewall that controls inbound and outbound traffic at the subnet level.

A ***security group*** is a virtual firewall that controls inbound and outbound traffic for an Amazon EC2 instance. By default, a security group denies all inbound traffic and allows all outbound traffic. You can add custom rules to configure which traffic should be allowed or denied.

>Security Groups and Network Access Control Lists are used to protect resources from traffic, and by themselves do not enable access to the internet - although they need to be properly configured to let traffic bound for the internet out.

A ***NAT Gateway*** is required to allow resources in a private subnet to access the internet. Route tables tell traffic where it should go next to reach its destination, but don't actually process or transmit traffic. 

#
***AWS Direct Connect*** is a service that enables you to establish a dedicated private connection between your data center and VPC.  The private connection that AWS Direct Connect provides helps you to reduce network costs and increase the amount of bandwidth that can travel through your network.

***AWS Snowball*** is a device that enables you to transfer large amounts of data into and out of AWS.
AWS Snowmobile is a service that is used for transferring up to 100 PB of data to AWS. Each Snowmobile is a 45-foot long shipping container that is pulled by a semi-trailer truck. 


The ***AWS Command Line Interface (AWS CLI)*** enables you to control multiple AWS services directly from the command line within one tool. For example, you can use comands to start an Amazon EC2 instance, connect an Amazon EC2 instance to a specific Auto Scaling group, and more. The AWS CLI is available for users on Windows, macOS, and Linux.

# Cost

***Cost Explorer*** is a free tool that you can use to view your costs. You can view data up to the last 13 months, forecast how much you are likely to spend for the next three months, and get recommendations for what Reserved Instances to purchase. You can use Cost Explorer to see patterns in how much you spend on AWS resources over time, identify areas that need further inquiry, and see trends that you can use to understand your costs. You also can specify time ranges for the data, and view time data by day or by month.
>With ***AWS Cost Explorer***, you can quickly create custom reports to analyze your AWS cost and usage data.

***AWS Budgets*** lets you set custom alerts that will notify you when your service usage exceeds (or is forecasted to exceed) the amount that you have budgeted.

***AWS Pricing Calculator*** lets you explore AWS services and create an estimate for the cost of your use cases on AWS. In the AWS Pricing Calculator, you can enter details for your cloud computing requirements and then receive a detailed estimate that can be exported and shared.

***Lightsail*** accomplishes Predicable monthly pricing and instance ability to burst above the baseline level of CPU performance when needed.

***AWS Budgets*** provides a useful feature of setting custom budgets that prompt the user when their costs or usage are forecasted to exceed. The forecast aspect gives a buffer period in advance when alerting the user. Budgets can be tracked at the monthly, quarterly, or yearly level, and have customizable start and end dates. Alerts can be sent via email and/or Amazon Simple Notification Service (SNS) topic.

# Message

***Amazon SQS*** is a message queuing service. Using Amazon SQS, you can send, store, and receive messages between software components at any volume size, without losing messages or requiring other services to be available. In Amazon SQS, an application sends messages into a queue. A user or service retrieves a message from the queue, processes it, and then deletes it from the queue.

# Instance Types
***Amazon EC2 Savings Plans*** enable you to reduce your compute costs by committing to a consistent amount of compute usage for a 1-year or 3-year term. This results in savings of up to 72% over On-Demand Instance costs. Any usage up to the commitment is charged at the discounted Savings Plan rate (for example, $10 an hour). Any usage beyond the commitment is charged at regular On-Demand Instance rates.

- ***Reserved Instances*** are a billing discount that is applied to the use of On-Demand Instances in your account. You can purchase Standard Reserved and Convertible Reservd Instances for a one-year or three-year term, and Scheduled Reserved Instances for a one-year term. Unlike Savings Plans, Reserved Instances do not require you to commit to a consistent amount of compute usage over the duration of the contract.

- ***Spot Instances*** are ideal for workloads with flexible start and end times or that can withstand interruptions. Spot Instances leverage unused EC2 computing capacity and offer you cost savings at up to 90% of On-Demand Instance prices.

- ***Dedicated Hosts*** are physical servers with EC2 instance capacity that is fully dedicated to your use. You can use your existing per-socket, per-core, or per-VM software licenses to help maintain license compliance. You can purchase On-Demand Dedicated Hosts or Reserved Dedicated Hosts. Of all the Amazon EC2 options that were covered in this course, Dedicated Hosts are the most expensive.
>Instance stores are ideal for temporary data that does not need to be kept long term. When an Amazon EC2 instance is stopped or terminated, all the data that has been written to the attached instance store is deleted.
  

# Database

>***Amazon ElastiCache*** is a service that adds caching layers on top of your databases to help improve the read times of common requests. A service that enables you to set up, manage, and scale a distributed in-memory or cache environment in the cloud -  *Amazon ElastiCache*.

***Amazon Redshift*** is a data warehousing service that you can use for big data analytics. It offers the ability to collect data from many sources and help you to understand relationships and trends across your data.

>Amazon Redshift provides the best solution for performing queries based on a predefined set of dimensions. Redshift organizes data for high performance based on user-specified distribution schemes.
 

>***Amazon DocumentDB*** is a document database service that supports MongoDB workloads.

***Amazon Quantum Ledger Database*** (Amazon QLDB) is a ledger database service. You can use Amazon QLDB to review a complete history of all the changes that have been made to your application data.

***Amazon DynamoDB*** is a key-value database service. A key-value database might include data pairs such as “Name: John Doe,” “Address: 123 Any Street,” and “City: Anytown”. In a key-value database, you can add or remove attributes from items in the table at any time. Additionally, not every item in the table has to have the same attributes.  

>Amazon Aurora is an enterprise-class relational database.Aurora is AWS' managed database service that is up to 5X faster than a traditional MySQL database.

>Amazon Relational Database Service (Amazon RDS) and Amazon Aurora use structured query language (SQL) to store and query data. They are not key-value databases.

***Amazon Neptune*** is a graph database service. You can use Amazon Neptune to build and run applications that work with highly connected datasets, such as recommendation engines, fraud detection, and knowledge graphs.

>Amazon Athena is a serverless query service used to analyze BigData stored in S3.

***Amazon Relational databases service (RDS)*** is best suited in scenarios where the dataset and forms are consistent such that their data schema is persistently valid. It is best to deploy in an environment where the load can be anticipated and is somewhat finite. Amazon RDS engines include Amazon Aurora, MariaDB, PostgreSQL.

>when an RDS Master database in a Multi-AZ deployment goes down RDS automatically fails over to the standby, which is promoted to Master.


# Compute

***Amazon EBS*** provides block-level storage volumes that you can use with Amazon EC2 instances. If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available.

>***Amazon EBS volumes*** are ideal for data that needs to be retained. When an Amazon EC2 instance is stopped or terminated, all of the data on the attached EBS volume is still available.

A service that monitors your applications and automatically adds or removes capacity from your resource groups in response to changing demand -  ***AWS Auto Scaling***.

***vertical scaling(scaling up)*** adds more resources to an instance and horizontal scaling(scaling out) adds more instances.

Leveraging ***AWS Lambda functions*** will remove the need to run a dedicated web server for the organisation. During periods of high requests to the database cluster, AWS lambda backend infrastructure will automatically scale out resources to adequately meet the demand. AWS Lambda provides a platform to run code without provisioning or managing any servers. The organisation pays only for the compute time they consume – there is no charge when your code is not running.
>***AWS Lambda*** is a service that lets you run code without provisioning or managing servers.

>The ***Classic loadbalancer*** uses a Round-Robin strategy for TCP listeners only.The ALB 1st selects a target based on the routing rule, then uses a Round-Robin strategy to select a node.

# Health

***AWS Personal Health Dashboard*** that focuses on the performance and availability of your AWS services so that you can respond accordingly. it displays their general status. The AWS Personal Health Dashboard publishes alerts and remediation guidance when issues with AWS services arise. Notifications are also provided for scheduled events that may impact AWS customers.

***Trusted Advisor*** provide best practices and/or or checks on Cost Optimization, Performance, Security, and Fault Tolerance. 

- To improve the ***performance*** of your services by providing recommendations for how to take advantage of provisioned throughput.

- The ***Security*** category includes checks that help you to review your permissions and identify which AWS security features to enable.

- The ***Cost Optimization*** category includes checks for unused or idle resources that could be eliminated and provide cost savings.

- The ***Fault Tolerance*** category includes checks to help you improve your applications’ availability and redundancy.






