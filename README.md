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


### Using

192.168.23.10 is the IP of the VM

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

By default, it uses an embedded database for storage. This is 'Ok' i feel for development purposes. Unless, you need more storage, advise you to configure an actual Database for storage. There are many web articles out there on how to do that.

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
[TBD]

#### GitList

There is additional first time configuration that is required.

Assuming you already have all your Git projects under /var/www/projects/ (checkout your projects into their).

1. Need to change /var/www/html's AllowOverride from None to All in the default Apache website config file
   (modify the /etc/httpd/conf/httpd.conf file)
2. Restart Apache
   (sudo apachectl restart)
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










