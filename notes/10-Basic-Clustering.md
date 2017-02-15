# Basic Clustering

- Till now we have 1 tomcat instance running and now we'll learn how to loadbalance multiple tomcat instances.
- For this let us have another tomcat instance configured first.
- Go to the ***/opt*** directory and copy ***tomcat8*** to ***tomcat8-n2***

```
# cp -prv tomcat8 tomcat8-n2
```

- Now we know that we are using some ports for tomcat say 8080, 8005, 8009
- For our additional tomcat instance we need to change the ports. If we don't then we might need to experience port conflict
- I am going to edit ***server.xml*** config file in the new node and increment the port numbers by 1

```
# cd /opt/tomcat8-n2/conf/
# vi server.xml

8005	->	8006
8080	->	8081
8443	->	8444
8009	->	8010
```

- Now you need to add your new Catalina home, base and temp directories
- First you need to change the ***catalina.sh*** script and redirect the above 3 variables to the new variables
- Edit the ***catalina.sh*** script and add the following lines

```
# vi /opt/tomcat-n2/bin/catalina.sh

CATALINA_BASE=$CATALINA_BASE2
CATALINA_HOME=$CATALINA_HOME2
CATALINA_TMPDIR=$CATALINA_TMPDIR2
```

- Now edit ***/etc/profile*** file and set our new directories

```
# vi /etc/profile

CATALINA_BASE2=/opt/tomcat8-n2
CATALINA_HOME2=/opt/tomcat8-n2
CATALINA_TMPDIR2=/opt/tomcat8-n2/temp
```

- Now we need to edit ***/etc/nginx/vhost.d/default.conf*** file to add the ***upstream*** directive to loadbalance
- Edit that file and add the following at the top of the file

```
upstream myTomcat {
	server localhost:8080;
	server localhost:8081;
}
```

- Now we need to change the proxy_pass

```
proxy_pass http://myTomcat;
```
