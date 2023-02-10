# Jenkins Installation

Jenkins is an open-source automation server that integrates with a number of AWS Services, including: AWS CodeCommit, AWS CodeDeploy, Amazon EC2 Spot, and Amazon EC2 Fleet. You can use Amazon Elastic Compute Cloud (Amazon EC2) to deploy a Jenkins application on AWS.

1. Open AWS console , Navigate to Create EC2 and select ubuntu free tier or Amazon Linux 2 AMI and use t2.small.
2. make sure your instnace security group has this Inbound Rules.
    ![Security Group](./images/securitygrp.jpg)
3. connect to instance using putty or ssh connect. 
4. Use the ssh command to connect to the instance. You will specify the private key (.pem) file and ec2-user@public_dns_name.

   ```console
   $ ssh -i /path/my-key-pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com
   ```

5. Ensure that your software packages are up to date on your instance by uing the following command to perform a quick software update:

   ```console
   [ec2-user ~]$ sudo yum update –y
   ```

6. Add the Jenkins repo using the following command:

   ```console
   [ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
   ```

7. Import a key file from Jenkins-CI to enable installation from the package:

   ```console
   [ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
   [ec2-user ~]$ sudo yum upgrade
   ```

8. Install Java:

   ```console
   [ec2-user ~]$ sudo amazon-linux-extras install java-openjdk11 -y
   ```

9. Install Jenkins

   ```console
   sudo yum install jenkins -y
   ```

10. Enable the Jenkins service to start at boot:

   ```console
   [ec2-user ~]$ sudo systemctl enable jenkins
   ```

11. Start Jenkins as a service:

   ```console
[ec2-user ~]$ sudo systemctl start jenkins
```

12. You can check the status of the Jenkins service using the command:

```console
[ec2-user ~]$ sudo systemctl status jenkins
```

* Jenkins is now installed and running on your EC2 instance. To configure Jenkins:
  * Connect to <http://<your_server_public_DNS>:8080> from your browser. You will be able to access Jenkins through its management interface:
   ![Unlock Jenkins](./images/unlockjenkins.jpg)
  * As prompted, enter the password found in /var/lib/jenkins/secrets/initialAdminPassword.Use the following command to display this password:

   ```console
   [ec2-user ~]$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   ```