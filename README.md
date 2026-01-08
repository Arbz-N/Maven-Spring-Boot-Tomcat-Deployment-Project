**Project Overview**

    This project demonstrates the complete lifecycle of a Java web application built using Spring Initializr, managed with Maven, and deployed in two ways:
    As a standalone JAR application
    As a WAR file deployed on Apache Tomcat

**It covers:**
    
    Project creation using Spring Initializr
    Maven build lifecycle
    Running application using java -jar
    Manual Tomcat installation & configuration
    Deploying WAR to Tomcat server
    This is a beginner-friendly but real DevOps-style workflow for Java web deployments.


**Prerequisites**

    Make sure you have:
    Linux machine (Ubuntu recommended)
    Java JDK installed
    Maven installed
    Internet access to download dependencies
    Basic Linux command knowledge

**Verify installations:**

    java -version
    mvn -version

**Build & Test with Maven**

Run the Maven lifecycle commands step by step: (go to the folder where pom.xml file is present)

    mvn clean     #delete the old build if any
    mvn compile   #code compile
    mvn test      #Tests run  
    mvn package   #make JAR/WAR file


After build, your artifact will be available in:

    target/
    Run as Standalone JAR
    java -jar target/your-file.jar


    Application will start on:
    http://localhost:8080

**Apache Tomcat Installation**
    Step 1 — Download & Extract
    cd /opt
    sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
    sudo tar -xvf apache-tomcat-9.0.65.tar.gz

**Configure Tomcat Users**

    Edit:
    sudo vi /opt/apache-tomcat-9.0.65/conf/tomcat-users.xml

    Add before closing tag:
    <user username="admin" password="admin1234" roles="admin-gui, manager-gui"/>

**Enable Remote Access to Manager App**

    Edit:
    sudo vi /opt/apache-tomcat-9.0.65/webapps/manager/META-INF/context.xml

    
    **Comment out this block:**

    <!--
    <Valve className="org.apache.catalina.valves.RemoteAddrValve"
     allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
    -->
    #by default tomcat can only be accessed by locahost if you comment this line out then
    #it will be accessed by remote browser
    # it is only for learning purpose

**Create Short Commands**

    sudo ln -s /opt/apache-tomcat-9.0.65/bin/startup.sh /usr/bin/startTomcat
    sudo ln -s /opt/apache-tomcat-9.0.65/bin/shutdown.sh /usr/bin/stopTomcat

**Fix Permissions** 

    sudo chown -R $USER:$USER /opt/apache-tomcat-9.0.65
    chmod +x /opt/apache-tomcat-9.0.65/bin/*.sh

**Start Tomcat**
    sudo startTomcat


Check:

    http://<server-ip>:8080

    Deploy WAR File
    
    Copy your WAR file:
    sudo cp target/*.war /opt/apache-tomcat-9.0.65/webapps/


**Tomcat will auto-deploy it.**

    Access your app:
    http://<server-ip>:8080/<app-name>

    Testing

    Tomcat Manager:

    http://<server-ip>:8080/manager


    Application URL:

    http://<server-ip>:8080/your-app

**Important Notes**

    Read every file before executing commands.
    Do NOT expose Tomcat manager on production without security hardening.
    Use strong passwords instead of demo credentials.
    Stop Tomcat when not in use.

**Cleanup Reminder**

    Don’t forget to delete all resources if you are deploying this project only for learning and practice.
    Leaving services running can cause unnecessary cost and security risks.