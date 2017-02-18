# Configuring Tomcat as Service

- Till now we are starting or stopping the tomcat instance from the home through the catalina script.
- We will not be able to start this through ***service*** or ***systemctl***
- In the previous sessions you might have seen that we have started this through ***service*** but it is a custom script written by me
- Apart from that we can't directly use tomcat through ***service***
- Now let us see how to accomplish this.
- For this we should have ***jvsc*** package installed on our ***CentOS/Redhat*** machine.
- This package will help us to run the java services as daemons or services.

	- Install through ***YUM***

	```
	# yum install jsvc -y
	```

	- If the packages are not available then we need to download and install from the source.

	> NOTE: Please ensure that you have configured you JAVA_HOME before proceeding with the below.

	```
	# wget http://www-eu.apache.org/dist//commons/daemon/source/commons-daemon-1.0.15-src.tar.gz
	# tar -xzvf commons-daemon-1.0.15-src.tar.gz
	# cd commons-daemon-1.0.15-src/src/native/unix
	# echo $JAVA_HOME
	# make
	# ./jsvc -help
	```

- Now we should have ***tomcat*** user and ***apache***

```
# useradd tomcat
# groupadd apache
# usermod -G apache tomcat
```

- Change the owner and group of the $CATALINA_HOME

> Before doing this be sure tomcat is not running. Stop if it is running

```
# cd /opt
# chown -R tomcat:apache tomcat8
```

- We need to create a file where our ENVIRONMENT variables can be setup for tomcat

```
# vi /etc/sysconfig/tomcat

CATALINA_HOME=/opt/tomcat8
JAVA_HOME=/opt/jdk8
JSVC=/usr/share/jsvc-src/commons-daemon-1.0.15-src/src/native/unix
```

- Now we need to create a service file for tomcat

```
# vi /usr/lib/systemd/system/tomcat.service

[Unit]
Description=Tomcat WebServer
After=syslog.target network.target

[Service]
Type=forking
User=tomcat
EnvironmentFile=/etc/sysconfig/tomcat
ExecStart=/opt/tomcat8/bin/catalina.sh start
ExecStop=/opt/tomcat8/bin/catalina.sh stop

[Install]
WantedBy=multi-user.target
```

- Enable the tomcat service

```
# systemctl enable tomcat.service
```

- Start Tomcat

```
# systemctl start tomcat.service
```

