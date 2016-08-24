# A Development Environment (operated by Vagrant)

An opinionated take on constructing a development environment to be used on a software project. Common softwares of technology, tools, toolkit have been selected for automatic provisioning by Vagrant.
Vagrant will manage the environment under which it starts up a VM (Virtual Machine) running CentOS as the base Operating System.

The following are provisioned:

- Java 8
- Git
- Maven
- Jenkins
- MySQL
- NGINX
- Apache Web Server
- Sonar (SonarQube Server)
- Sonar Runner (Sonar Analyser)
- Nexus
- GitList

All running within a centOS VM.


### Detailed Information

| Tool   | Description                                            |
|:-------|:-------------------------------------------------------|
| Java 8 | Programming Language                                   |
| Git    | SCM (Source Code Management System)/ VCS (Version Control System) |
| Maven  | Build Tool (Project Management Tool)                   |
| Jenkins | Continous Integration (CI) Server                     |
| Sonar    | Code Quality Analysis Toolkit                        |
| Nexus    | Artefacts Repository Manager                         |
| GitList   | Open Source Git Repository Viewer (built in PHP)    |
| MySQL    | Relational Database                                  |
| Apache   | Http Web Server                                      |
| NGINX    | Web Server/Reverse Proxy                             |


### Usage

192.168.23.10 is the IP of the VM

If you don't like the IP you can change this, just edit it in the `Vagrantfile`

```
vagrant up
```
ssh into it
```
vagrant ssh
```
it might be necessary to switch to root user

```
sudo su -
```

#### Java

Checking the version of Java installed simply do:

```
java --version
```

#### Maven

To check for the maven install simply do

```
which mvn
```

which will tell you where the binaries executable are

just use maven as you would normally

#### Git

```
which git
```

will tell you where Git has been installed to

#### Jenkins

Jenkins 2 is installed

Open your browser locally and navigate to http://192.168.23.10:6060/

which will direct you to the Jenkins getting started configuration wizard on startup. Here you can select which jenkins plugins you want 
and configure it the way you want to use Jenkins. Then just use Jenkins as you normally would do:

- set up build jobs etc...

#### Sonar (SonarQube Server)

It should already be started. If not run the following command:

```
sudo /opt/sonar/bin/linux-x86-64/sonar.sh start
```

this will start up the Sonar server.

Alternatively,

```
sudo /opt/sonar/bin/linux-x86-64/sonar.sh console
```

Terminal output console will display whether Sonar was successfully started or not.
Once started, you can browse to

http://192.168.23.10:9000

in order to access Sonar admin web user interface which from there you can configure and setup projects to be analysed.

Please consult the Sonar official documentation on how to use this.

By default, it uses an embedded database for storage. This is 'OK' i feel for development purposes. Unless, you need more storage, advise you to configure an actual Database for storage. There are many web articles out there on how to do that.

default login credentials:

Username: admin  
Password: admin

#### Sonar Runner

There are a number of different ways in which you can analyse your projects using Sonar. One option is to let Maven the build tool run the analyse as part of its build process which you can easily set up by hooking up the maven-sonar-plugin.

Another option is to manually run the analyse of your projects using the Sonar Runner.

To do this, place a sonar-properties file on the root of your project directory.

Then just run the Sonar Runner:

e.g.

```
/opt/sonar-runner/
```

#### Nexus
Nexus is your repository manager that allows you to store your project artifacts. This is a place where you can upload, download, and browse all your project artifacts in one place via a web user interface. 

Simply navigate to:

http://192.168.23.10:8081/nexus/#welcome

Note, you might need to do some minor configuration upon first use, just consult online Nexus user guide/reference manual for more information. But most of the time, probably just configure your maven build to upload your built and packaged artifacts to nexus. 
Check maven user manual for more information on this.

#### GitList

There is additional first time configuration that is required.

Assuming you already have all your Git projects under /var/www/projects/ (checkout your projects into there).

1. Need to change /var/www/html's AllowOverride from None to All in the default Apache website config file
   (modify the /etc/httpd/conf/httpd.conf file)
2. Restart Apache   
   ```
   sudo apachectl restart  
   ```   
3. reboot VM   
    ```
    vagrant halt
    ```  
    then   
    ```
    vagrant up
    ```   
    again   
    
After restarting...

navigate to http://192.168.23.10/gitlist/

and you should list of your Git projects


#### MySQL

This is an opinionated take on a development environment. With the assumption of your project using a MySQL database it is up to you on how to use it. So you can configure this Database as you will just like you normally do as per your project needs.

#### Tomcat

This is an opinionated take on a development environment. Tomcat 7. Not the latest version of Tomcat. Is is with the assumption that your project uses Apache Tomcat the open source Web (Servlet) Container. Most projects are web applications and runs on this Servlet container. It is there if you need it. However, it is not common for projects to use an embedded tomcat from maven-tomcat7-plugin.

#### Apache
This is an opinionated take on a development environment. Apache Http Web Server is provided if you ever really need it. However, it is to note that GitList the Git Repository Viewer runs on Apache so this is needed.


#### NGINX
This is an opinionated take on a development environment. NGINX is a very modern popular web server which commonly used as a load balancer or reverse forward proxying. Either way, this is there if you require it and up to you how you use it.








