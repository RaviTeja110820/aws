# Run Infra as Code with Jenkins

# Steps
1. Install Jenkins
   - Marketplace AMI (Free!)
2. Install CloudFormation Plugin
3. Run Cft using Cft plugin
4. Run Cft Jenkins pipeline
    - Uses AWS CLI Commands

# Setup

## To Install Jenkins
1. Jenkins certified by Bitnami
2. password = select instance ->Actions ->Instance settings -> Get system Log
3. Copy the public Ip f Instance and paste in the Browser.
4. Install Suggested plugins
5. manage jenkins -> manage pugins : search for cludformation plugin and install withoout restart.
6. git hub with cloudformation template, that contains s3 Bucket code.
7. 