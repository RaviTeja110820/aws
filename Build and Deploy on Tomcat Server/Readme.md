# Build and Deploy Artifacts on Tomcat Server
when a developer commits code through git to github then a pipeline is triggered in the jenkins, then maven starts build the code, finally the arifact is deployed on tomcat server.


![Architecture](./images/architecture.png)
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

## Create a CI and CD Job
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

3. install maven in ec2 instnace:
    ```console
    sudo -i

    cd /opt/

    sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo

    sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo

    sudo yum install -y apache-maven

    mvn –version
    ```

4. now open the jenkins-> manage jenkins -> Global tool configuration -> maven:
   * Add maven
   * name - local_maven  #what we mentioned in pipeline
   * maven home - /opt/maven

5. Now upload your java code in repositry. Refer to my code through this link https://github.com/RaviTeja110820/devopsweb/tree/test1

## Test the Deployment.

6. Click on build now and if all stages are succeded you can see like.
   ![pipelineBuild](./images/pipelineBuild.jpg)

7. now go to browser and type ipaddress/8090/devopsweb then you will see your java application page, thats it done.
   ![Devopsweb page](./images/devopswebpage.jpg)

8. To trigger the pipeline automatically when you commit and push code. follow this link - https://github.com/RaviTeja110820/aws/tree/Devops-Projects/Run%20Infra%20as%20Code%20with%20Jenkins  and see for trigger job