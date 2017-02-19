# Running Multiple Tomcat Instances on a Single Server Setup

- Be sure you have installed JDK-8 and check the following variables

```
# env | grep JAVA
JAVA_HOME=/opt/jdk8

# env | grep JRE
JRE_HOME=/opt/jdk8/jre
```

- Add ***tomcat*** user and group

```
# groupadd tomcat
# useradd -M -s /sbin/nologin -g tomcat -d /opt/tomcat tomcat
```

- Have the tomcat base downloaded to your machine and extreact those to ***/opt/tomcat-src***
- In my case I already have tomcat downloaded. So I am going to extract those

```
# mkdir /opt/tomcat-src
# tar -xzvf ~/apache-tomcat-8.5.11.tar.gz -C tomcat-src/ --strip-components=1
```

- Let us create 2 directories for our tomcat instances

```
# mkdir /opt/tomcat{1,2}
```

- Copy the contents of ***tomcat-src*** to ***tomcat1*** and ***tomcat2***

```
# cp -prf /opt/tomcat-src/* /opt/tomcat1
# cp -prf /opt/tomcat-src/* /opt/tomcat2
```

- Let us change the permissions of some directories in ***tomcat1*** and ***tomcat2***

```
# cd tomcat1/
# chgrp -R tomcat conf
# chmod g+rwx conf/
# chmod g+r conf/*
# chown -R tomcat work/ temp/ logs/
```

```
# cd tomcat2/
# chgrp -R tomcat conf
# chmod g+rwx conf/
# chmod g+r conf/*
# chown -R tomcat work/ temp/ logs/
```

- Now we need to change the configs to change the ports as we know each instance should have some distinct ports to listen on.

```
[TOMCAT1]

Shutdown Port	->      7005
Web Port		->      7080
Redirect Port	->      7443
AJP Conn. Port	->      7009
```

```
[TOMCAT2]

Shutdown Port   ->      8005
Web Port        ->      8080
Redirect Port   ->      8443
AJP Conn. Port  ->      8009
```

- Please refer to [Basic Clustering](10-Basic-Clustering.md) to know how to change the ports also to know how can these tomcat instances be run in a clustered environment to balance the load
