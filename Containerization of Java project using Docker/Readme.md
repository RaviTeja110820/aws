# Containerization of Java project using Docker

In this project we gonna fetch source code from a Git repository, creating Docker workflows, writing Dockerfiles, building images, and pushing customized Docker images to Docker Hub.

Firstly, we will retrieve the source code from the Git repository and create a Docker workflow. To customize the services, namely nginx, Tomcat, and MySQL, we will need to write three Docker files. After writing the Docker files in the source code, we will use the Docker build command on the Docker engine, mentioning the base image in the Docker files. The base images, namely Tomcat, Nginx, and MySQL, will be pulled from Docker Hub, and we will customize them. Using the Docker build command, our images will be built by reading the Docker files. After our images are ready, we will use Docker Compose to mention all the containers with the images and test them. Once it passes the testing, we will push the customized Docker images to Docker Hub under our own account.

![Architecture flow](./images/architecture.jpg)

## Steps

1. Steps to setup our stack services
2. Find right Base image from dockerhub
3. Write Dockerfile to customize images
4. Write docker-compose.yml file to run multi containers.
5. Test it & Host Images on Dockerhub

## setup

1. Launch an Instance:
   * Name : Docker-project
   * Ami : Ubuntu
   * Instance type : t2.micro
   * Key pair : ci-vprofile-key
   * Security Group : vprofile-docker-sg
2. Login to the instance 

### Install Docker in the instance

1. to install docker follow the below steps or you can go to the docker official website and install

   ```console
   $ sudo apt update
   $ sudo apt install docker.io -y
   $ docker --version
   $ sudo systemctl status docker
   $ sudo systemctl start docker
   $ sudo usermod -aG docker ubuntu    # now logout from instance and login again
   $ docker run hello-world
   $ docker images
   ``` 

### Docker Hub

1. if you don't have docker hub account create it <https://hub.docker.com/>
2. we need three images so click on create repository:
   * Name : vprofiledb
     * public -> create
     * this is for mysql
   * Name : vprofileweb
     * public -> create
     * this is for nginx
   * Name : vprofileapp 
     * public -> create
     * this is for Tomcat image