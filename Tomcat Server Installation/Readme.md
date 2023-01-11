# Tomcat Server Installation on EC2 Instance

## Pre-requisites
1. EC2 instance with Java 11

## Install Apache Tomcat

1. Download tomcat packages from https://tomcat.apache.org/download-80.cgi onto /opt on EC2 instance
    > Note: Make sure you change <version> with the tomcat version which you download.
2. Login to the instance and run below commands:
    ```console
    $ sudo su -               # switch to root user
    # hostname tomcat   # changeing the hostname to tomcat
    # sudo su -         # Refreshing so you  can see the tomcat as user name
    # cd /opt           # moving to directory *opt*
    # wget http://mirrors.fibergrid.in/apache/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.tar.gz   # tomcat installatin link

    # ls           # it will list the files in the directory
    # tar -xvzf apache-tomcat-8.5.43.tar.gz  # unzip and untar
    # mv apache-tomcat-8.5.43 tomcat        # Renaming to tomcat
    
    ```
3. To start the tomcat server
   ```console
    # cd /opt/tomcat/
    # cd bin/
    # ls
    # ./startup.sh       # to start the tomcat server
    # ./shutdown.sh      # to stop the tomcat server     
   ```
4. The default port for tomcat server is 8080, and also if we run jenkins in same instance its default port will be also 8080. so to not cause any issue we will change the port of Tomcat server to 8090. Change port number in conf/server.xml file under tomcat home.
   ```console
   # cd /opt/tomcat/conf      # update port number in the "connecter port" field in server.xml & restart tomcat after configuration update
   # cd /opt/tomcat/bin
   # ./shutdown.sh
   # ./startup.sh
   ```  
    ![Change Port](./images/portchange.jpg)
5. Now to access the tomcat server go to webbrowser and type instnaceIP:8090
6. click on Manager Apps, you get an 403 Access Denied. By default the tomcat server allows us from your local system, To address this issue we need to update configuration file context.xml.
    ![apache page](./images/tomcatpage.jpg)
7. To resolve the error:
     ```console
    # find  / -name context.xml
    ```
    i. After Running above command you get some related files , you need to edit all the files that were in the webapps directory.
    ii. Edit the files ,open each and every file,  goto "value classname" line and comment it. in linux we can comment a line using <!-- some text -->.
        ![comment](./images/comment.jpg)
    iii. After that now shutdown and start the tomcat server.
8. now go to Apache Tomcat page and click on Manager Apps. Then it asks for username and password.
    
    ![sigin](./images/sigin.jpg)
9. to get username and password, Update users information in the tomcat-users.xml file goto tomcat home directory and Add below users to conf/tomcat-users.xml file
    ```console
    <role rolename="manager-gui"/>
    <role rolename="manager-script"/>
    <role rolename="manager-jmx"/>
    <role rolename="manager-status"/>
    <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
    <user username="deployer" password="deployer" roles="manager-script"/>    #jenkins
    <user username="tomcat" password="s3cret" roles="manager-gui"/>           # tomcat
    ```
    ![Tomcat usres](./images/tomcat%20users.jpg)
    ![Tomcat user login page](./images/username.jpg)