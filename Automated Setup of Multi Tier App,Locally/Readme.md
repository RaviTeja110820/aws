# Automated Setup of Multi Tier App Locally

In this project we use bash scripts to provision the servers.

![Automation-arch](./images/automation-arch.jpg)

# setup

1. clone the project into your Drive using the below command in cmd or git bash

   ```console
   $ git clone https://github.com/RaviTeja110820/vprofile-project.git
   ```

2. now execute the below commands:

   ```console
   $ ls
   $ cd vprofile-project/
   $ ls
   $ git checkout local-setup
   $ cd vagrant/
   $ cd Automated_provisioning/
   $ ls
   $ cat Vagrantfile       # to view
   ```

3. to execute follow below commands:

   ```console
   $ vagrant up
   
   ```

## verify

Now login nginx server and run command ifconfig and copy the ip address paste in browser.

* username and password are same - admin_vp
  
```console
$ vagrant destroy           # to delete the vagrant file
```
