# Oracle Java 8 - Inatallation & Setup

- Download Oracle JDK 8 or later from Oracle site.

```
# cd /opt/
# wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u121-b13/e9e7ea248e2c4826b92b3f075a80e441/jdk-8u121-linux-x64.tar.gz"
# tar xzf jdk-8u121-linux-x64.tar.gz
# mv jdk1.8.0_121/ jdk8/
```

- Install Java with Alternatives

```
# cd /opt/jdk8
# alternatives --install /usr/bin/java java /opt/jdk8/bin/java 2
# alternatives --config java

# alternatives --install /usr/bin/jar jar /opt/jdk8/bin/jar 2
# alternatives --set jar /opt/jdk8/bin/jar

# alternatives --install /usr/bin/javac javac /opt/jdk8/bin/javac 2
# alternatives --set javac /opt/jdk8/bin/javac
```

- Check the installation

```
# java -version
# javac -version
```


- Now we have Oracle Java 8 ready as a pre-requisite of Tomcat 8

- Configuring Environment variables
	- Setup JAVA_HOME
	
	```
	# export JAVA_HOME=/opt/jdk8
	```

	- Setup JRE_HOME
	
	```
	# export JRE_HOME=/opt/jdk8/jre
	```

	- Setup PATH

	```
	# export PATH=$PATH:/opt/jdk8/bin:/opt/jdk8/jre/bin
	```
