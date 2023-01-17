# Run Infra as Code with Jenkins

# Steps
1. Install Jenkins
   - Marketplace AMI (Free!)
2. Install CloudFormation Plugin
3. Run Cft using Cft plugin
4. Install AWS CLI
   - SSH and Install AWS CLI 
   - Use SSM Session Manager to Install without any keys
5. Jenkins File
6. IAM Role for EC2
7. Run Cft Jenkins pipeline
    - Uses AWS CLI Commands
8. Trigger job

# Setup

## To Install Jenkins
1. Create Instance -> click on Browse mor AMI's and search for Jenkins packaged by Bitnami,select it.
   ![Jenkins Bitnami](./images/jenkinsBitnami.jpg)
2. select keypair, Reamining all leave as default and launch the instance.
   
3. password = select instance ->Actions ->Instance settings -> Monitor and troubleshoot -> Get system Log. Wait for some time to load the log files , then copy the password and username from the log file, As shown in below image.
   ![username and Password](./images/userpass.jpg)
4. Copy the public Ip of Instance and paste in the Browser. Now enter the copied username and password. Then you can see the jenkins Dashboard after sigin.
   
   ![sigin](./images/sigin.jpg)
5. Install Suggested plugins - Git, Pipeline , Build
6. manage jenkins -> manage plugins : search for cloudformation plugin and install without restart.
7. create a git hub Repositry with cloudformation template, that contains s3 Bucket code.
   ```json
   {
    "AWSTemplateFormatVersion": "2010-09-09",
    "Resources": {
        "S3Bucket": {
            "Type": "AWS::S3::Bucket"
        }
    },
    "Outputs": {
        "BucketName": {
            "Value": {
                "Ref": "S3Bucket"
            },
            "Description": "Name of the sample Amazon S3 bucket."
        }
    }
    }
    ```

## Run Cft using Cft plugin
1. In jenkins -> create new job -> name : cftdemo-jenkinsplugin -> FreestyleProject
2. In source code managemment Select git:
    * Paste the source code url in Repositry URL
    * credintals - Add jenkins, and give github username and Password.
    * after that select the credentials.
    ![Source Code Management](./images/sourcecodemanagement.jpg)
3.  Build Environment -> Select Create AWS Cloud Formation stack.
    * Cloud Formation recipe file -> filename.json that you used in 6th point
    * stack name -> jenkinscftplugin-s3
    * Now create an IAM user with s3 and cloudFormation Permissions(Programmatic access) in AWS Console.
    * Enter AWS access key and secret access key.
4. click save.
5.  click on Build Now, click on no-1 and select console output
6.  Go to cloud Formation in aws and check the output. Click on events then you can see that s3 Bucket create complete. Now go to s3 Bucket and confirm that.

## Install AWS CLI
1. search for AWS Systems Manager in console.
2. remote connect -> Explore session manager
3. click on start session and select the jenkins instance -> start session.
4. now run the below commands:
```console
$ sudo apt-get update
$ sudo apt-get install awscli
$ aws configure                 # give accesskey and secret accesskey Id, Region, format - Json
```
## jenkins file
```yaml
pipeline {
    agent any
    stages {
        stage('Submit Stack') {
            steps {
            sh "aws cloudformation create-stack --stack-name s3bucket --template-body file://simplests3cft.json --region 'us-east-1'"
              }
        }
    }
}
```

## IAM Role for EC2
1. select the jenkins instance .
2. open the IAM Role in new tab.
3. click on Attach policy:
   - AWSCloudFormationFullAccess
   - s3FullAccess

## Run Cft Jenkins pipeline
1. in Jenkins Dashboard click on new item.
2. name - pipeline-s3-cft, and select pipeline,click ok
   - go to pipeline - select pipeline script from SCM
   - SCM -> Git ->paste the repositry url, give the credentials
   - script path -> Jenkinsfile
   - click on save
3. click on Build Now
4. goto console output
5. goto cloud formation in consle and u can see the s3 bucket created. 

## Trigger job
![Triggerd Stack](./images/triggeredstack.jpg)
1. goto job , click configure
2. Build trigger -> select Github hook trigger for GITScm polling and click save.
3. Goto your repository , click on settings tab.
4. click on webhooks -> Add webhook:
   - PayloadUrl - jenkins dashboard url/github-webhook/
   - content type - application/json
   - just the push event
   - Add Webhook
5. Remove the output in the s3 bucket and commit changes.
6. Come back to the jenkins job. Then you can see new build happens. also check the consle output.