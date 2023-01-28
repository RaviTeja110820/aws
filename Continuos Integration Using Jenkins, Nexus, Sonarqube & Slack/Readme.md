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