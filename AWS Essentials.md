# Security
***AWS GuardDuty*** is a service that provides intelligent threat detection for your AWS infrastructure and resources. AWS GuardDuty identifies threats by continually monitoring the network activity and account behavior within your AWS environment.


***AWS Shield*** is a managed DDoS protection service that is available in two tiers: Standard and Advanced. AWS Shield Standard applies always-on detection and inline mitigation techniques, such as deterministic packet filtering and priority-based traffic shaping, to minimize application downtime and latency. AWS Shield Standard is included automatically and transparently to your Elastic Load Balancing load balancers, Amazon CloudFront distributions, and Amazon Route 53 resources at no additional cost. When you use these services that include AWS Shield Standard, you receive comprehensive availability protection against all known infrastructure layer attacks. Customers who have the technical expertise to manage their own monitoring and mstigation of application layer attacks can use AWS Shield together with AWS WAF rules to create a comprehensive DDoS attack mitigation strategy.
>***AWS Shield*** is a service that helps protect your applications against distributed denial-of-service (DDoS) attacks .

***AWS Shield*** – All AWS customers benefit from the automatic protections of AWS Shield Standard, at no additional charge. AWS Shield Standard defends against most common, frequently occurring network and transport layer DDoS attacks that target your web site or applications.
***AWS Shield Advanced*** – For higher levels of protection against attacks targeting your web applications running on Amazon EC2, Elastic Load Balancing (ELB), CloudFront, and Route 53 resources, you can subscribe to AWS Shield Advanced. AWS Shield Advanced provides expanded DDoS attack protection for these resource

***Amazon Inspector*** is a service that checks applications for security vulnerabilities and deviations from security best practices.Amazon Inspector enables you to analyze the behavior of your AWS resources and helps you to identify potential security issues. Using Amazon Inspector, you can define a collection of AWS resources that you want to include in an assessment target. You can then create an assessment template and launch a security assessment run of this target.

***AWS Artifact*** provides on-demand downloads of AWS security and compliance documents, such as AWS ISO certifications, Payment Card Industry (PCI), and Service Organization Control (SOC) reports. You can submit the security and compliance documents (also known as audit artifacts) to your auditors or regulators to demonstrate the security and compliance of the AWS infrastructure and services that you use.
>***AWS Artifact*** is a service that enables you to access AWS security and compliance reports and special online agreements.

***AWS Artifact*** is a comprehensive resource center for access to AWS’ auditor issued reports as well as security and compliance documentation from several renowned independent standards organisations.


# Cloud Trail
With ***CloudTrail***, you can view a complete history of user activity and API calls for your applications and resources.  Events are typically updated in CloudTrail within 15 minutes after an API call was made. You can filter events by specifying the time and date that an API call occurred, the user who requested the action, the type of resource that was involved in the API call, and more.

>By viewing Event history in Amazon CloudTrail, the administrator can be able to access operational, access and activity logs for the past 90 days, to the S3 bucket that hosts the static website


***AWS CloudTrail*** is a service that primarily tracks governance, compliance, operational auditing, and risk auditing of your AWS account. CloudTrail logs continuously monitors, and retains account activity related to actions across all AWS infrastructure. CloudTrail provides event history of AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and troubleshooting.

# AWS CloudWatch 
***Amazon CloudWatch*** is a service that provides data that you can use to monitor your applications, optimize resource utilization, and respond to system-wide performance changes.

An alarm in ***AWS CloudWatch*** that triggers after exceeding the bill will not meet the requirements of staying within the desired budget. The alarm triggers when the account billing exceeds the threshold specified. It triggers only when actual billing exceeds the threshold.

# Global Infrastructure
***Availability Zone*** is a single data center or a group of data centers within a Region.  Availability Zones are located tens of miles apart from each other. This helps them to provide interconnectivity to support the services and applications that run within a Region.
>There are atleast *3 Availability Zones* per AWS Region. Some regions may contain more.

>A separate geographical location with multiple locations that are isolated from each other  ***Region.***

>The server from which Amazon CloudFront gets your files  ***origin***.

>A site that Amazon CloudFront uses to cache copies of content for faster delivery to users at any location - ***Edge location***.
A *Distribution* is made up of Edge Locations that you want to serve content from, and details about how that content will be tracked an managed.

***Amazon CloudFront*** is a content delivery service. It uses a network of edge locations to cache content and deliver content to customers all over the world. When content is cached, it is stored locally as a copy. This content might be video files, photos, webpages, and so on.

>Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, to your users. 

***AWS Infrastructure Event Management (IEM)*** offers architecture and scaling guidance and operational support during the preparation and execution of planned events, such as shopping holidays, product launches, and migrations. For these events, AWS Infrastructure Event Management will help you assess operational readiness, identify and mitigate risks, and execute your event confidently with AWS experts by your side. The program is included in the Enterprise Support plan and is available to Business Support customers for an additional fee.

# Plans
The ***AWS Free Tier*** is not a Support plan. It is a program that consists of three types of offers that allow customers to use AWS services without incurring costs: Always free, 12 months free, and Trials.
#
***Amazon Route 53*** is a DNS web service. It gives developers and businesses a reliable way to route end users to internet applications that are hosted in AWS. Additionally, you can transfer DNS records for existing domain names that are currently managed by other domain registrars, or register new domain names directly within Amazon Route 53.
>In Amazon Route 53, the **geolocation routing policy** allows for different resources to serve content based on the origin of the request. This in turn makes it possible in the scenario for different versions of the website to be served.
Amazon Route 53 geolocation routing policy makes it possible for different types of content to be served depending on the geographical location of where the browser is

>When a Disaster does occur , it can be easy to switch to secondary sites using the Route53 service

>In Amazon Route53 any alterations made to record sets in hosted zones will take the duration of the set Time to live (TTL) before they can reflect. However, flushing of the local DNS and browser cache will prompt a new query to the Route53 hosted zone thereby giving the new changes.

>***Fail over Routing policy*** will make it possible for traffic to be routed to the resource in good health and not to the one experiencing poor response times.


#
***Refactoring*** is migration strategy involves changing how an application is architected and developed, typically by using cloud-native features.

***AWS Database Migration Service (DMS)*** helps you migrate databases to AWS quickly and securely. The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database. The AWS Database Migration Service can migrate your data to and from most widely used commercial and open-source databases.
>- AWS DMS can migrate databases from on-premise to AWS 
>-  AWS DMS can migrate databases from EC2 to Amazon RDS
>-   AWS DMS can migrate databases from AWS to on-premise 
>-   AWS DMS can have Amazon Redshift and Amazon DynamoDB as target databases

***Repurchasing*** involves replacing an existing application with a cloud-based version, such as software found in AWS Marketplace.

**Rehosting** involves moving an application to the cloud with little to no modifications to the application itself. It is also known as “lift and shift.”

***Replatforming*** involves selectively optimizing aspects of an application to achieve benefits in the cloud without changing the core architecture of the application. It is also known as “lift, tinker, and shift.”

>AWS permits users to conduct ***vulnerability and penetration testing*** certain specified AWS services. This allows organisations to comply with any industry regulations that stipulate that vulnerability and penetration testing be conducted on services and infrastructure.

# S3
In the ***S3 Intelligent-Tiering*** storage class, Amazon S3 monitors objects’ access patterns. If you haven’t accessed an object for 30 consecutive days, Amazon S3 automatically moves it to the infrequent access tier, S3 Standard-IA. If you access an object in the infrequent access tier, Amazon S3 automatically moves it to the frequent access tier, S3 Standard.

>Data is organised in S3 into **Archives**, and **Vaults** are used to group Archives together. **Access policies** control who can access the data in Archives & Vaults.

***S3 Glacier*** is a low-cost storage class that is ideal for data archiving. You can retrieve objects stored in the S3 Glacier storage class within a few minutes to a few hours.
>AWS Console cannot be used to upload data onto Glacier. The console can only be used to create a Glacier vault which can be used to upload the data.%0D%0AFor more information on uploading data onto Glacie

The ***S3 Standard-IA*** storage class is ideal for data that is infrequently accessed but requires high availability when needed. Both S3 Standard and S3 Standard-IA store data in a minimum of three Availability Zones. S3 Standard-IA provides the same level of availability as S3 Standard but at a lower storage price. 

***S3 One Zone-IA*** is ideal for infrequently accessed data that does not require high availability.

>***Amazon Elastic Transcoder*** lets you convert media files that you have stored in Amazon Simple Storage Service (Amazon S3) into media files in the formats required by consumer playback devices.

***Amazon Simple Storage Service (Amazon S3)*** is a service that provides object-level storage. Amazon S3 stores data as objects within buckets.
>*Amazon S3 buckets* cannot be attached to Amazon EC2 instances.


>***Access Control Lists*** let you control access to individual objects within an S3 bucket, where as ***Bucket Policies*** allow you to control access to entire buckets. In relation to S3.

>AWS has updated the URL format for objects in S3 in order to partition the name space. This will introduce more consistency, but be aware that there are still multiple variation depending on feature and location. - *https, then the bucket name, then dot, then the AWS S3 regional endpoint, then slash, then the object name.*

**S3 Intelligent-Tiering** is the first cloud object storage class that delivers automatic cost savings by moving data between two access tiers — frequent access and infrequent access — when access patterns change, and is ideal for data with unknown or changing access patterns.S3 Intelligent-Tiering stores objects in two access tiers: one tier that is optimized for frequent access and another lower-cost tier that is optimized for infrequent access. For a small monthly monitoring and automation fee per object, S3 Intelligent-Tiering monitors access patterns and moves objects that have not been accessed for 30 consecutive days to the infrequent access tier. There are no retrieval fees in S3 Intelligent-Tiering. If an object in the infrequent access tier is accessed later, it is automatically moved back to the frequent access tier. No additional tiering fees apply when objects are moved between access tiers within the S3 Intelligent-Tiering storage class. S3 Intelligent-Tiering is designed for 99.9% availability and 99.999999999% durability, and offers the same low latency and high throughput performance of S3 Standard.

>**Amazon S3 Transfer Acceleration** enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket. Transfer Acceleration takes advantage of Amazon CloudFront’s globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path.

>***AWS DataSync*** Can copy data between NFS servers, SMB file shares, Amazon S3 buckets, and Amazon EFS file system. it is a fully managed data transfer service with built-in retry mechanism.It is integrated with AWS CloudWatch

# Well Architected Frame Work
The ***Performance Efficiency pillar*** focuses on using computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.

The ***Operational Excellence pillar*** includes the ability to run workloads effectively, gain insights into their operations, and continuously improve supporting processes to deliver business value. 

The ***Security pillar*** focuses on protecting data, systems, and assets. It also focuses on using cloud technologies to improve the security of your workloads.

The ***Reliability pillar*** focuses on the ability of a workload to consistently and correctly perform its intended functions.

# AWS Organizations
In ***AWS Organizations***, you can centrally control permissions for the accounts in your organization by using service control policies (SCPs). Additionally, you can use the consolidated billing feature in AWS Organizations to combine usage and receive a single bill for multiple AWS accounts.

***AWS Organizations*** allows the user to automate the creation of new AWS accounts when they need to quickly launch new workloads. The administrator can add these new accounts to user-defined groups in an organization for easy categorization. For example, you can create separate groups to categorize development and production accounts, and then apply a Service Control Policy (SCP) to the production group allowing only access to AWS services required by production workloads.


# Networking
A virtual private gateway enables you to establish a virtual private network (VPN) connection between your VPC and a private network, such as an on-premises data center or internal corporate network.
> A *virtual private gateway* allows traffic into the VPC only if it is coming from an approved network.

>***AWS Transit Gateway*** routes all traffic to and from each VPC or VPN, and you have one place to manage and monitor it all. 

An ***internet gateway*** is a connection between a VPC and the internet. It allows public traffic from the internet to access a VPC.

A ***subnet*** is a section of a VPC in which you can group resources based on security or operational needs.

Provision an isolated section of the AWS Cloud to launch resources in a virtual network that you define  ***Amazon Virtual Private Cloud (Amazon VPC)***.

>A *network access control list (ACL)* is a virtual firewall that controls inbound and outbound traffic at the subnet level.

***VPC Peering*** can be established between VPCs in different AWS Regions and in separate AWS Accounts. The logical networks still use the same common AWS backbone network infrastructure to communicate. By utilizing this infrastructure, VPC Peering makes it possible to securely store mission-critical data to geographically distinct locations for fault-tolerance, disaster recovery and redundancy.

A ***security group*** is a virtual firewall that controls inbound and outbound traffic for an Amazon EC2 instance. By default, a security group denies all inbound traffic and allows all outbound traffic. You can add custom rules to configure which traffic should be allowed or denied.

>Security Groups and Network Access Control Lists are used to protect resources from traffic, and by themselves do not enable access to the internet - although they need to be properly configured to let traffic bound for the internet out.

A ***NAT Gateway*** is required to allow resources in a private subnet to access the internet. Route tables tell traffic where it should go next to reach its destination, but don't actually process or transmit traffic. 

>A service that lets you monitor network requests that come into your web applications - ***AWS WAF***.

***AWS Web Application Firewall (WAF)*** is a web-based application that allows for monitoring of ingress and egress traffic on provisioned web services. These could be in an AWS CloudFront distribution, behind an AWS Load Balancer or standalone instance. AWS WAF includes AWS Shield (AWS Shield Standard that comes at no additional cost and AWS Shield Advanced, on subscription) that protects against SYN floods, DNS query floods and UDP reflection attacks amongst others.

***AWS Global Accelerator*** is a networking service that improves the performance of your users' traffic by up to 60% using Amazon Web Services' global network infrastructure. When the internet is congested, AWS Global Accelerator optimizes the path to your application to keep packet loss, jitter, and latency consistently low.

# Transfer
***AWS Direct Connect*** is a service that enables you to establish a dedicated private connection between your data center and VPC.  The private connection that AWS Direct Connect provides helps you to reduce network costs and increase the amount of bandwidth that can travel through your network.

***AWS Snowball*** is a device that enables you to transfer large amounts of data into and out of AWS.
AWS Snowmobile is a service that is used for transferring up to 100 PB of data to AWS. Each Snowmobile is a 45-foot long shipping container that is pulled by a semi-trailer truck. 

>***AWS Outposts*** is a service that enables you to run infrastructure in a hybrid cloud approach.

***AWS Local Zones*** are a type of AWS infrastructure deployment that place compute, storage, database, and other select services closer to large population, industry, and IT centers, enabling you to deliver applications that require single- digit millisecond latency to end-users.

> **Run low-latency** applications at the edge Build and deploy applications close to end users to enable real-time gaming, live streaming, augmented and virtual reality (AR/VR), virtual workstations, and more. Simplify hybrid cloud migrations Migrate your applications a near by while still meeting the low-latency requirements of hybrid deployment.

>***AWS Snowball*** is a device that enables you to transfer large amounts of data into and out of AWS.

***Amazon Kinesis Data Streams (KDS)*** is a massively scalable and durable real-time data streaming service…. The data collected is available in milliseconds to enable real-time analytics use cases such as real-time dashboards, real-time anomaly detection, dynamic pricing, and more.

>If you want a fully managed solution and you want to use SQL to process the data from your data stream, you should use ***Kinesis Data Analytics***.

***Amazon Kinesis Client Library (KCL)*** is a service to process and query streaming data using SQL KCL is more complicated than AWS Kinesis Data Analytics. “Kinesis Data Analytics uses the KCL to read data from streaming data sources as one part of your underlying application. The service abstracts this from you, as well as many of the more complex concepts associated with using the KCL, such as checkpointing”

>***Amazon Kinesis Data Firehose*** is a service for loading data streams.

The ***AWS Command Line Interface (AWS CLI)*** enables you to control multiple AWS services directly from the command line within one tool. For example, you can use comands to start an Amazon EC2 instance, connect an Amazon EC2 instance to a specific Auto Scaling group, and more. The AWS CLI is available for users on Windows, macOS, and Linux.

# Cost

***Cost Explorer*** is a free tool that you can use to view your costs. You can view data up to the last 13 months, forecast how much you are likely to spend for the next three months, and get recommendations for what Reserved Instances to purchase. You can use Cost Explorer to see patterns in how much you spend on AWS resources over time, identify areas that need further inquiry, and see trends that you can use to understand your costs. You also can specify time ranges for the data, and view time data by day or by month.
>With ***AWS Cost Explorer***, you can quickly create custom reports to analyze your AWS cost and usage data.

***AWS Budgets*** lets you set custom alerts that will notify you when your service usage exceeds (or is forecasted to exceed) the amount that you have budgeted.

***AWS Pricing Calculator*** lets you explore AWS services and create an estimate for the cost of your use cases on AWS. In the AWS Pricing Calculator, you can enter details for your cloud computing requirements and then receive a detailed estimate that can be exported and shared.

>***Lightsail*** accomplishes Predicable monthly pricing and instance ability to burst above the baseline level of CPU performance when needed.

***AWS Budgets*** provides a useful feature of setting custom budgets that prompt the user when their costs or usage are forecasted to exceed. The forecast aspect gives a buffer period in advance when alerting the user. Budgets can be tracked at the monthly, quarterly, or yearly level, and have customizable start and end dates. Alerts can be sent via email and/or Amazon Simple Notification Service (SNS) topic.

***AWS Support Concierge*** Included as part of the Enterprise Support plan, the Support Concierge Team are AWS billing and account experts that specialize in working with enterprise accounts.

# Message

***Amazon SQS*** is a message queuing service. Using Amazon SQS, you can send, store, and receive messages between software components at any volume size, without losing messages or requiring other services to be available. In Amazon SQS, an application sends messages into a queue. A user or service retrieves a message from the queue, processes it, and then deletes it from the queue.
>Amazon Simple Queue Service (Amazon SQS) offers a reliable, highly-scalable hosted queue for storing messages as they travel between applications or microservices. It moves data between distributed application components and helps you decouple these components.

***AWS SQS*** implements messaging that is a typical integration pattern to decouple application components. AWS documentation mention it “Amazon SQS offers a reliable, highly-scalable hosted queue for storing messages as they travel between applications or microservices. It moves data between distributed application components and helps you decouple these components. “

# Instance Types
***Amazon EC2 Savings Plans*** enable you to reduce your compute costs by committing to a consistent amount of compute usage for a 1-year or 3-year term. This results in savings of up to 72% over On-Demand Instance costs. Any usage up to the commitment is charged at the discounted Savings Plan rate (for example, $10 an hour). Any usage beyond the commitment is charged at regular On-Demand Instance rates.

- ***Reserved Instances*** are a billing discount that is applied to the use of On-Demand Instances in your account. You can purchase Standard Reserved and Convertible Reservd Instances for a one-year or three-year term, and Scheduled Reserved Instances for a one-year term. Unlike Savings Plans, Reserved Instances do not require you to commit to a consistent amount of compute usage over the duration of the contract.

- ***Spot Instances*** are ideal for workloads with flexible start and end times or that can withstand interruptions. Spot Instances leverage unused EC2 computing capacity and offer you cost savings at up to 90% of On-Demand Instance prices.

- ***Dedicated Hosts*** are physical servers with EC2 instance capacity that is fully dedicated to your use. You can use your existing per-socket, per-core, or per-VM software licenses to help maintain license compliance. You can purchase On-Demand Dedicated Hosts or Reserved Dedicated Hosts. Of all the Amazon EC2 options that were covered in this course, Dedicated Hosts are the most expensive.
>***Instance stores*** are ideal for temporary data that does not need to be kept long term. When an Amazon EC2 instance is stopped or terminated, all the data that has been written to the attached instance store is deleted.

***Amazon Machine Image (AMI)*** provides the information required to launch an instance, which is a virtual server in the cloud. You specify an AMI when you launch an instance, and you can launch as many instances from the AMI as you need. You can also launch instances from as many different AMIs as you need
  

# Database

***Amazon ElastiCache*** is a service that adds caching layers on top of your databases to help improve the read times of common requests. A service that enables you to set up, manage, and scale a distributed in-memory or cache environment in the cloud -  *Amazon ElastiCache*.

>implementing and configuring Amazon ElastiCache will improve the performance by storing frequently accessed content in-memory. The storage type is a managed, high-speed, volatile and not disk-based, making information retrieval faster than disk-based stored content.


***Amazon Redshift*** is a data warehousing service that you can use for big data analytics. It offers the ability to collect data from many sources and help you to understand relationships and trends across your data.

>Amazon Redshift provides the best solution for performing queries based on a predefined set of dimensions. Redshift organizes data for high performance based on user-specified distribution schemes.
 

>***Amazon DocumentDB*** is a document database service that supports MongoDB workloads.

***Amazon Quantum Ledger Database*** (Amazon QLDB) is a ledger database service. You can use Amazon QLDB to review a complete history of all the changes that have been made to your application data.

***Amazon DynamoDB*** is a key-value database service. A key-value database might include data pairs such as “Name: John Doe,” “Address: 123 Any Street,” and “City: Anytown”. In a key-value database, you can add or remove attributes from items in the table at any time. Additionally, not every item in the table has to have the same attributes.  
>the most appropriate attribute of Amazon DynamoDB is its flexible data model and single-digit millisecond latency

***Amazon Aurora (Aurora)*** is a fully managed, MySQL- and PostgreSQL-compatible, relational database engine. It combines the speed and reliability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases. It delivers up to five times the throughput of MySQL and up to three times the throughput of PostgreSQL without requiring changes to most of your existing applications.

>Amazon Aurora is an enterprise-class relational database.Aurora is AWS' managed database service that is up to 5X faster than a traditional MySQL database.

>Amazon Relational Database Service (Amazon RDS) and Amazon Aurora use structured query language (SQL) to store and query data. They are not key-value databases.

***Amazon Neptune*** is a graph database service. You can use Amazon Neptune to build and run applications that work with highly connected datasets, such as recommendation engines, fraud detection, and knowledge graphs.

***Amazon Athena*** a serverless query service that does not need to build databases on dedicated Elastic Block Store (EBS) volumes, instead, it builds tables from data read directly from Amazon S3 buckets. Amazon Athena does not store any of the data. The service is compatible with the regular data formats that include CSV, JSON, ORC, AVRO and Parquet
>Amazon Athena is a serverless query service used to analyze BigData stored in S3.

***Amazon Relational databases service (RDS)*** is best suited in scenarios where the dataset and forms are consistent such that their data schema is persistently valid. It is best to deploy in an environment where the load can be anticipated and is somewhat finite. Amazon RDS engines include Amazon Aurora, MariaDB, PostgreSQL.

>when an RDS Master database in a Multi-AZ deployment goes down RDS automatically fails over to the standby, which is promoted to Master.

You can reduce the load on your source DB Instance by routing read queries from your applications to the read replica. ***Read replicas*** allow you to elastically scale out beyond the capacity constraints of a single DB instance for read-heavy database workloads

>***Read replicas*** will enhance the database performance and durability by allowing for automated distribution of load amongst several database instances with the exact copy of the parent database.


# Compute

***Amazon EBS*** provides block-level storage volumes that you can use with Amazon EC2 instances. If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available.

>***Amazon EBS volumes*** are ideal for data that needs to be retained. When an Amazon EC2 instance is stopped or terminated, all of the data on the attached EBS volume is still available.

A service that monitors your applications and automatically adds or removes capacity from your resource groups in response to changing demand -  ***AWS Auto Scaling***.

>***vertical scaling(scaling up)*** adds more resources to an instance and ***horizontal scaling(scaling out)*** adds more instances.

>The concept of ***Elasticity*** is the means of an application having the ability to scale up and scale down based on demand. An example of such a service is the Autoscaling service.

***AWS Lambda*** is a service that lets you run code without needing to provision or manage servers. While using AWS Lambda, you pay only for the compute time that you consume. You are charged only when your code is running. With AWS Lambda, you can run code for virtually any type of application or backend service, all with zero administration. 

Leveraging ***AWS Lambda functions*** will remove the need to run a dedicated web server for the organisation. During periods of high requests to the database cluster, AWS lambda backend infrastructure will automatically scale out resources to adequately meet the demand. AWS Lambda provides a platform to run code without provisioning or managing any servers. The organisation pays only for the compute time they consume – there is no charge when your code is not running.
>***AWS Lambda*** is a service that lets you run code without provisioning or managing servers.

A ***load balancer*** acts as a single point of contact for all incoming web traffic to your Auto Scaling group. This means that as Amazon EC2 instances are added or removed in response to the amount of incoming traffic, these requests are routed to the load balancer first and then spread across multiple resources that will handle them

>The ***Classic loadbalancer*** uses a Round-Robin strategy for TCP listeners only.The ALB 1st selects a target based on the routing rule, then uses a Round-Robin strategy to select a node.

***AWS Lambda@Edge*** is a serverless service that makes it possible to run event-triggered functions on Edge Locations within the AWS Content Delivery Network. Using AWS CloudFront, an administrator can introduce decision-making and compute processing closer to the viewer’s location, thereby improving on their browsing experience.

# Health

***AWS Personal Health Dashboard*** that focuses on the performance and availability of your AWS services so that you can respond accordingly. it displays their general status. The AWS Personal Health Dashboard publishes alerts and remediation guidance when issues with AWS services arise. Notifications are also provided for scheduled events that may impact AWS customers.

***AWS Trusted Advisor*** is an online tool that inspects your AWS environment and provides real-time guidance in accordance with AWS best practices.

>*Enterprise and Business* Support plans include access to all AWS Trusted Advisor checks. The *Basic and Developer* Support plans provide access to a limited selection of AWS Trusted Advisor checks.



>Trusted Advisor provide best practices and/or or checks on *Cost Optimization, Performance, Security, and Fault Tolerance.*


- To improve the ***performance*** of your services by providing recommendations for how to take advantage of provisioned throughput.

- The ***Security*** category includes checks that help you to review your permissions and identify which AWS security features to enable.

- The ***Cost Optimization*** category includes checks for unused or idle resources that could be eliminated and provide cost savings.

- The ***Fault Tolerance*** category includes checks to help you improve your applications’ availability and redundancy.

# Manager

***AWS Systems Manager*** allows users to gain control of their AWS resources by unifying services into a user interface. One in which they can be able to view, automate and monitor operational tasks.

***Resource Access Manager (AWS RAM)*** allows users to share resources with other AWS accounts or via AWS Organizations. AWS RAM can be used to collate a set of AWS resources across multiple AWS
accounts in order to share capacity.

The ***AWS Certificate Manager*** allows the web administrator to maintain one or several SSL/TLS certificates, both private and public certificates, including their update and renewal such that the administrator does not worry about imminent expiry of certificates.

AWS ***Lifecycle Manager*** serves the purpose of creating lifecycle policies for specified resources in order to automate operations.

AWS ***License Manager*** serves the purpose of differentiating, maintaining third-party software provisioning vendor licenses as well as decreases the risk of license expirations and the penalties.

AWS ***Firewall Manager*** aids in the administration of Web Application Firewall (WAF), by presenting a centralised point of setting firewall rules across different web resources.

***Technical Account Manager (TAM)*** is your designated technical point of contact who helps you onboard, provides advocacy and guidance to help plan and build solutions using best practices, coordinates access to subject matter experts, assists with case management, presents insights and recommendations on your AWS spend, workload optimization, and event management, and proactively keeps your AWS environment healthy.

>A resource that provides guidance, architectural reviews, and ongoing communication with your company as you plan, deploy, and optimize your applications - ***Technical Account Manager (TAM).*** 


# Code 

***AWS CodeCommit*** is a managed source control service that can be used as a data store to store source code, binaries, scripts, HTML pages and images which are accessible over the internet. CodeCommit encrypts files in transit and at rest.

***AWS CodeStar*** provides a unified user interface, enabling you to easily manage your software development activities in one place. With AWS CodeStar, you can set up your entire continuous delivery toolchain in minutes, allowing you to start releasing code faster. AWS CodeStar makes it easy for your whole team to work together securely, allowing you to easily manage access and add owners, contributors, and viewers to your projects.

***AWS CodeDeploy*** is a deployment service that allows developers to automate the installation of applications to hosts, Amazon EC2 instances, Amazon ECS instances, serverless Lambda functions or even on-premises servers. AWS CodeDeploy can enable the update of those applications.

***AWS X-Ray*** helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, developers can understand how the application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through an application, and shows a map of an application’s underlying components.
>**AWS X-Ray** provides a complete view of requests as they travel through your application and filters visual data across payloads, functions, traces, services, APIs, and more with no-code and low-code motions.

# Advanced

***AWS OpsWorks*** provides a fully managed configuration automation and management service of Chef and Puppet. These platforms will allow for the use of code to automate the configuration of the EC2 instances, including replication as stated in the scenario. With Chef and Puppet, OpsWorks allows for the automation of how servers are configured, deployed, and managed across Amazon EC2 instances or on-premises compute environments.

>Automate the deployment of workloads into your AWS environment - ***AWS Quick Starts***.

***Amazon Rekognition*** enables the uptake of imagery and video for analysis in applications. By uploading imagery or video footage to the Rekognition API, the service engine would then identify and distinguish facial features, text, objects and activities. This service will meet the requirements of the scenario as an access control solution.

>***Amazon Comprehend*** uses natural language processing (NLP) to extract insights about the content of documents.

The entire concept of ***decoupling components*** is to ensure that the different components of an applications can be managed and maintained separately. If all components are tightly coupled then when one component goes down , the entire application would do down. Hence it is always a better design practice to decouple application components.

***Amazon QuickSight*** is a fully-managed service that allows for insightful business intelligence reporting, with creative methods of data delivery including graphical and interactive dashboards. QuickSight includes machine learning which allows users to discover inconspicuous trends and patterns on their datasets.

>***Amazon Polly*** uses deep learning technologies to synthesize natural-sounding human speech, so you can convert articles to speech. With dozens of lifelike voices across a broad set of languages, use Amazon Polly to build speech-activated applications.

***AWS CloudFormation*** provides templates to specify all the AWS resources needed by the testing environments. These templates can be instantiated as stacks to provision consistent environments every time one is needed.

>Provision resources by using programming languages or a text file - AWS CloudFormation.

You upload your application, and ***Elastic Beanstalk*** automatically handles the deployment details of capacity provisioning, load balancing, auto-scaling, and application health monitoring.

***Amazon EMR*** helps you analyze and process vast amounts of data by distributing the computational work across a cluster of virtual servers running in the AWS Cloud. The cluster is managed using an open-source framework called Hadoop. Amazon EMR lets you focus on crunching or analyzing your data without having to worry about the time-consuming setup, management, and tuning of Hadoop clusters or the compute capacity they rely on.

***Amazon EKS*** is a fully managed service that you can use to run Kubernetes on AWS. Kubernetes is open-source software that enables you to deploy and manage containerized applications at scale. Containers provide you with a standard way to package your application's code and dependencies into a single object. Containers are frequently used for processes and workflows in which there are essential requirements for security, reliability, and scalability.

***Amazon Augmented AI (Amazon A2I)*** provides built-in human review workflows for common machine learning use cases, such as content moderation and text extraction from documents. With Amazon A2I, you can also create your own workflows for machine learning models built on AmazonA2I

>***Amazon SageMaker*** is a service that enables you to quickly build, train, and deploy machine learning models.***AWS DeepRacer*** is an autonomous 1/18 scale race car that you can use to test reinforcement learning models.

***Amazon Macie*** is a fully managed security service that uses AI and ML to continuously observe data access activity in order to alert the user of any anomalies if they arise. Alerts may include unauthorized access, data leaks and any out-of-the-norm patterns. The major functions are to discover, classify and protect the user data.

>Using artificial intelligence (AI), machine learning (ML), natural language understanding (NLU), ***Amazon Macie*** has the capability to read documents and sift through user data for sensitive or vulnerable information that can be exploited. Information such as credit/debit card numbers, access keys in documents will trigger an alert. Amazon Macie integrates with Amazon CloudTrail to detect unusual access patterns to user data and alerts the administrator.

# Perspective

The ***Operations Perspective*** of the AWS Cloud Adoption Framework also includes principles for operating in the cloud by using agile best practices.

The ***Business Perspective*** helps you to move from a model that separates business and IT strategies into a business model that integrates IT strategy.

The ***People Perspective*** helps Human Resources (HR) employees prepare their teams for cloud adoption by updating organizational processes and staff skills to include cloud-based competencies.

The ***Governance Perspective*** helps you understand how to update the staff skills and organizational processes that are necessary to ensure business governance in the cloud.

# Resource And Service

>You can use ***AWS Marketplace*** to find, test, and buy software that runs on AWS. A digital catalog that includes thousands of software listings from independent software vendors.

A resource that can answer questions about best practices and assist with troubleshooting issues -  ***AWS Support***.

The ***AWS Resource Center*** a repository of tutorials, whitepapers, digital trainings and project Use cases that aid in learning the core concepts of Amazon Web Services.

***AWS Directory Service*** is an AWS tool that provides multiple ways to use Amazon Cloud Directory and Microsoft Active Directory with other AWS services

***Amazon Cognito web identity federation*** service acts as a broker that allows successfully authenticated users access to AWS resources. After successful authentication on platforms such as Facebook, LinkedIn or Google – users are awarded temporary authentication code from Amazon Cognito thereby gaining temporary access.

***Resource Tags*** are user-defined label that has a key-value pair of variable character length. It is assigned to AWS resources as metadata for administration and management purposes.

***AWS Identity and Access Management (IAM)*** is a service that you can use to manage access to AWS services and resources. 

***Access Analyzer*** helps you identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, shared with an external entity. This lets you identify unintended access to your resources and data, which is a security risk.

***IAM Identity Federation*** allows access to the AWS environment using a central single sign-on (SSO) set of credentials from third-party or corporate active directory. Federation uses open standards such as SAML2.0 to transact identity information between identity provider (IdP) the respective applications

***AWS Key Management Service (AWS KMS)*** enables you to create, manage, and use cryptographic keys.This service is used for creating and managing of keys and control the use of encryption across a wide range of AWS services and in your applications. The basic usage of this to protect the data at various stages like in-transit, rest, etc..

***AWS Config*** service allows the administrator to monitor and record configuration changes on AWS resources in their account. The service also allows the administrator to create a resource configuration inventory.

>***AWS Config*** can be used to keep track of configuration changes on AWS resources, keeping multiple date-stamped versions in a reviewable history.

***AWS Managed Service Providers (MSP)*** provide end-to-end AWS solutions to customers at any stage of the cloud journey-from consultation on initial solution design, to building applications, through to ongoing optimization and support. By working with next-generation AWS MSP Partners, you can leverage the cloud as a strategic business advantage that goes beyond technical benefits and generates positive business outcomes. AWS MSPs are your trusted advisors and support customers of all sizes with different business needs.

# Dont Know which service
***Quotas***, also referred to as limits in AWS services, are the maximum values for the resources, actions, and items in your AWS account. Each AWS service defines its quotas and establishes default values for those quotas. Depending on your business needs, you might need to increase your service quota values.

# Disaster Recovery
![Disaster Recovery](disaster-recovery-strategies.png)

