# Build and Deploy Artifacts on Tomcat Server

# Steps
1. Setup Jenkins
2. Setup & Configure Maven , Git
3. Setup Tomcat Server
4. Integrating GitHub,Maven ,Tomcat Server with Jenkins
5. Create a CI and CD Job
6. Test the Deployment.
   
# Setup

## Setup Jenkins
1. To install jenkins on EC2 switch to branch Jenkins Installation or follow the link - https://github.com/RaviTeja110820/aws/tree/Devops-Projects/Jenkins%20Installation

## Setup & Configure Maven , Git
1. Install git in the instance using the below command:
   ```console
    $ sudo yum install git
    $ git --version
   ```

## Setup Tomcat Server
To Install Tomcat server on EC2 switch to branch Tomcat server Installation or follow th link - https://github.com/RaviTeja110820/aws/tree/Devops-Projects/Tomcat%20Server%20Installation

## Integrating GitHub,Maven ,Tomcat Server with Jenkins
1. Login to Jenkins -> Create Item 
2. name - build-n-deploy, select pipeline:
   * Description - Build the java application and deploy into tomcat server
   * pipeline - pipeline Script from SCM
     * SCM - git
     * repositry url - github repositry url
      > if the above mentioned git repositry is public then no need mention the credentials of the github account.
     * to generate the pipeline code for tomcat click on pipeline syntax:
        * In snippet generator: 
           1. select Deploy war to container
           2. War file name - **/*.war
           3. Add container - select the tomcat version
           4. add the tomcat credentials
           5. tomcat url - http//Ipadresss:8090/
           6. generate the snippet , copy it and paste in deploy to tomcat build section in pipeline code.
           7. The pipeline script is saved with name Jenkinsfile
      > install plugin AWS CODE DEPLOY 