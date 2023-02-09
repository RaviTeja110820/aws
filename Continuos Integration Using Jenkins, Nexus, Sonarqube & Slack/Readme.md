# Continuos Integration Using Jenkins, Nexus, Sonarqube & Slack

![Architecture flow](./images/arcitecture%20flow.jpg)

The developer makes a code change and commits it. The commit is then synced with the remote repository using GitHub. As soon as GitHub receives the commit, the continuous integration server Jenkins detects it and fetches the latest code. Jenkins has an integration with GitHub. Jenkins then runs some code tests (unit tests). If there are any failures, a message is sent to Slack. If the tests pass, code analysis is done using Checkstyle and SonarQube scanner. This generates reports that are published on the SonarQube server. The server displays the results and also has quality gates. If the code passes the quality criteria, it moves to the next stages, else a failure notification is sent and execution stops. Once the code analysis is done, an artifact is built using the Maven build tool. If there are any build failures, a notification is sent. While the source code is being built, it needs certain Maven dependencies which are stored in the Nexus repository. Once the artifact is packaged, it is uploaded back to the Nexus Sonatype repository.

![Architecture](./images/architecture.jpg)

# Steps

1. Create login key
2. Create SG
   * jenkins
   * Nexus
   * Sonar
3. Create Ec2 instances with user data
   * jenkins
   * Nexus
   * Sonarqube
4. Jenkins post Installation
5. Nexus Repository setup
6. Sonarqube post installation
7. Jenkins Steps
   * Build Job
   * Setup Slack Notification
   * Checkstyle Code analysis
   * Setup Sonar Integration 
   * Sonar code analysis job
   * Artifact upload job
8. Connect All jobs together with BuildPipeline
9. Set Automatic build trigger

# setup

## Key pair

1. Go key pair in aws console
2. click on create key pair:
   * Name : ci-vprofile-key
   * format : .pem
   * click on create key pair

## Security Groups

1. security group for jenkins
   * Name : vprofile-jenkins-sg
   * Description : Security group for jenkins
   * inbound rules:
     * Custom TCP : 8080 : MYIP
     * Custom TCP : 22 : MYIP
     * All Traffic : add vprofile-sonar-sg , description : Allow sonar to access jenkins for quality gates result 
2. security group for Nexus server
   * Name : vprofile-nexus-sg
   * Description : Security group for Nexus
   * inbound rules:
     * Custom TCP : 8081 : MYIP
     * Custom TCP : 22 : MYIP
     * Custom TCP : 8081 : add vprofile-jenkins-sg , description : jenkins can upload artifact to nexus server
3. security group for SonarQube
   * Name : vprofile-sonar-sg
   * Description : Security group for sonar
   * inbound rules:
     * Custom TCP : 80 : MYIP
     * Custom TCP : 80 : add vprofile-jenkins-sg , description : jenkins can upload reports to sonar server

## Launch Instances

we need launch three instance and we need to provision them by providing user data. goto this repository to get the user data for the instances <https://github.com/RaviTeja110820/vprofile-project/tree/ci-jenkins/userdata>

1. Instance for jenkins:
   * Name : Jenkins-Server
   * Ami : Ubuntu 18
   * Instance type : t2.small
   * Key pair : ci-vprofile-key
   * Security Group : vprofile-jenkins-sg
   * user data : copy the user data from above given link and paste here
2. Instance for Nexus:
   * Name : Nexus-Server
   * Ami : Centos7
   * Instance type : t2.small or t2.medium
   * Key pair : ci-vprofile-key
   * Security Group : vprofile-nexus-sg
   * user data : copy the user data from above given link and paste here
3. Instance for SonarQube:
   * Name : sonarqube-Server
   * Ami : Ubuntu 18
   * Instance type : t2.medium
   * Key pair : ci-vprofile-key
   * Security Group : vprofile-sonar-sg
   * user data : copy the user data from above given link and paste here

### Post Installation of Jenkins

1. Copy the jenkins-server instance public ip and paste in the browser "publicIP:8080". If provision is completed we can see the login page and we need to do post installation of jenkins now.
2. login to the jenkins-server instance now.
3. run the below commands to get the initial password to login to jenkins:

   ```console
   $ sudo -i                                                    # be the root user
   $ cat /var/lib/jenkins/secrets/initialAdminPassword          # copy the password
   ```

4. paste the password in the jenkins login page:
   * install suggested plugins : yes
   * give username and some password
   * finally click on start using jenkins

### Post Installation of Nexus

1. Copy the Nexus-server instance public ip and paste in the browser "publicIP:8081"
2. click on sign in and copy the password path.
3. Log into the Nexus Server
4. run the below commands to get the password to login to Nexus:  

   ```console
   $ sudo -i                                                    # be the root user
   $ cat /opt/nexus/sonatype-work/nexus3/admin.password          # copy the password
   ```

5. in Nexus user name : admin and paste the password you copied.
6. It will asks for a new password.
   * click on Enable anonymous access

7. click on settings -> Repository -> Repositories -> click on create Repository
   * select Maven2(hosted)
     * Name : vprofile-release         # for uploading Artifact
     * create Repository
   * select maven2(proxy)
     * Name : vpro-maven-central       # it stores maven dependencies
     * proxy -> remote storage : <https://repo1.maven.org/maven2/>          # from this url it downloads the maven dependencies and store it in this repository
     * click on create repository
   * select Maven2(hosted)
     * Name : vprofile-snapshot
     * change version policy : snapshot
     * create Repository
   * select maven2(group)
     * Name : vpro-maven-group              # it groups the two repository
     * Group -> member Repositories -> add vpro-maven-central, vprofile-release and vprofile-snapshot to members by clicking the arrows.
     * click on create repository.

> in source code, goto settings.xml file, you can see that there are variables that denotes the Repositories created in Nexus. Thus maven will get information about dependencies through them. 


### Build & Nexus Integration Job

1. Go To jenkins , click on create job:
   * Name : Build
   * select Freestyle project
     * in Source code management select Git
       * paste the repository url <https://github.com/devopshydclub/vprofile-project.git>
       * Branch specifier : */ci-jenkins
     * click on build ->  select Invoke top-level Maven targets:
       * Goals : install -DskipTests              # it will build the artifact without running the tests
       * click on Advanced
       * In properties paste the below variables and change according to your nexus repository names and ip:

         ```console
         SNAP-REPO=vprofile-snapshot
         NEXUS-USER=admin
         NEXUS-PASS=admin123
         RELEASE-REPO=vprofile-release
         CENTRAL-REPO=vpro-maven-central
         NEXUS-GRP-REPO=vpro-maven-group
         NEXUSIP= mention privateIP of Nexus-server instance
         NEXUSPORT=8081
         ```

         The above variables contains the nexus repository Names and also it password, username,private ip. 
       * click on Settings file -> select Settings file in filesystem 
         * File path : settings.xml 

     * save it 

2. click on Build Now
   * check the logs
   * to verify go to Nexus Repository -> browse -> select the repository then you can see the dependencies

### Slack Integration

1. create a workspace in the slack with the name Devops projects.
2. Create a channel in the workspace with name vprofile-jenkins.
3. Go to <https://api.slack.com/> to create a bot:
   * click on start building:
     * click on your Apps on top right -> select create your first App -> From scratch
     * App name : Jenkins , select your workspace : Devops projects
     * click on create App
     * Now Go to OAuth & Permissions -> find Bot Token Scopes -> click on Add an OAuth Scope -> choose chat:write 
     * now scroll up and click on install to workspace and say Allow. 
     * now you will get an ***Bot User OAuth Token*** , copy it and save some where 
4. Go to vprofile-jenkins channel in slack and type app name that is @Jenkins and click on Add to channel . Thats it
5. Lets integrate our slack bot with jenkins:
   * goto jenkins and click on manage jenkins -> manage plugins : 
     * search for slack notification and click on install without restart
   * jenkins -> manage jenkins -> manage credentials : 
     * jenkins -> Global credentials -> Add credentials:
       * Kind : secret text
       * Secret : paste the Bot User OAuth Token that you saved earlier
       * ID : slack-token
       * Description : slack-token
       * click ok
   * jenkins -> manage jenkins -> configure system -> slack settings:
     * Enable custom slack app bot user
     * click on save
6. goto the build job that was created earlier :
   * click on configure:
     * goto post-build Actions and select slack notification : enable for Notify Build start, Notify success, Notify Unstable, Notify Every Failure.
     * click on goto Advanced :
       * Workspace : Devops projects
       * credential : slack-token
       * Channel : #vprofile-jenkins
       * click on Test connection and if it shows success , everything ok else you need to very above steps again.
     * goto post-build Actions and select Archive Artifact:
       * Files to archive : **/*.war
     * Save
      >> Goto slack then you can see a message in the channel 
   * click on Build now 

7. Goto slack then you can see a Notifications in the channel

### Test 

1. Go To jenkins , click on create job:
   * Name : Test
   * select Freestyle project
   * copy from Build
   * click ok
     * click on build -> goals : test
     * Advanced settings : remove the archive, we dona need that war file now.
   * save
2. click on build now. It will run the unit test cases. 
3. lets integrate both build and test jobs. 
   * goto build job -> click on configure:
     * Add post build actions -> choose build other project:
     * project to build -> Test
4. Go To jenkins , click on create job:
   * Name: Integration Test
   * select Freestyle project
   * copy from Test 
   * click ok
     * click on build -> goals : verify -DskipUnitTests
     * save

5. Goto Test job -> click on configure:
   * Add post build actions -> choose build other project:
   * project to build -> Integration Test
   * save
6. Goto Integration Test job -> click on Build Now
7. Now we have integrated three jobs.

