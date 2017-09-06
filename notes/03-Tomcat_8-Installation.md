# Apache Tomcat 8 Installation

- Download Tomcat 8

```
# wget http://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.11/bin/apache-tomcat-8.5.11.tar.gz
# tar -xzvf apache-tomcat-8.5.11.tar.gz
# mv apache-tomcat-8.5.11/ tomcat8
```

- Export the Environment Variables

```
# cd /opt/tomcat8/bin
# export CATALINA_HOME=/opt/tomcat8/
```

- Now start the Tomcat application using ***startup.sh*** located within ***bin*** directory of CATALINA_HOME

```
# cd $CATALINA_HOME/bin
# ./startup.sh
```

- Check Tomcat process

```
# ps -ef | grep catalina | grep -v grep 
# netstat -ant | grep 8080 | grep -v grep
```
