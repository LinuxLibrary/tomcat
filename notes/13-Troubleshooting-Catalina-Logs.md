# Troubleshooting Tomcat using Catalina log

- We can get the ***catalina*** logs in ***$CATALINA_HOME/logs***
- Here we'll have a ***catalina.out***
- We can see some huge info in that log file. If we want to what exactly happens since the start of tomcat then we need to log that into a new file.
- By default we have log rotation enabled on this logs.
- For now let us stop tomcat and nullify the catalina.out file and then start tomcat to have some new info in the catalina.out

```
# service tomcat stop
# cd $CATALINA_HOME/logs
# :> catalina.out (or) cat /dev/null > catalina.out
# ll catalina.out
-rw-r----- 1 root root 0 Feb 18 16:19 catalina.out

# service tomcat start
# ll catalina.out
-rw-r----- 1 root root 17341 Feb 18 16:21 catalina.out
```

- We can see the log being written after the start of tomcat.
- Now we can notice the instance giving some information about the starting of tomcat, about the configuration for the startup, path of the servlet instance for which the log is responsible for, when the instance and the webapplications have started.
- Also as we are not hosting any production applications on it we don't have any other information logged continuously to it as there is no running transaction on it.
- And the last line in this log at this moment tells us how much time the tomcat instance has took to startup.
- We can see how the issues can be logged in this log file.
- As we previously configured another tomcat instance with some different port numbers let us change the config file of the first instance to use the connector port as ***8010***
- Let us stop the tomcat instance, do the above change, start the second instance and then start the first instance.

	```
	# cd $CATALINA_HOME
	# ./bin/catalina.sh stop
	# :> logs/catalina.out
	# vi conf/server.xml
	```

	- Change port 8009 with 8010 and save the config file

	```
	# cd $CATALINA_HOME2
	# ./bin/catalina.sh start
	# ps -ef | grep catalina | grep -v grep
	# cd $CATALINA_HOME
	# ./bin/catalina.sh start
	# ps -ef | grep catalina | grep -v grep
	```

	- We can see 2 tomcat instances running, let us check the ***catalina.out*** log for the errors. We will see the following error in the log.

	```
	18-Feb-2017 16:39:33.802 SEVERE [main] org.apache.catalina.core.StandardService.initInternal Failed to initialize connector [Connector
	[AJP/1.3-8010]]
	org.apache.catalina.LifecycleException: Failed to initialize component [Connector[AJP/1.3-8010]]
			at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:112)
			at org.apache.catalina.core.StandardService.initInternal(StandardService.java:549)
			at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:107)
			at org.apache.catalina.core.StandardServer.initInternal(StandardServer.java:875)
			at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:107)
			at org.apache.catalina.startup.Catalina.load(Catalina.java:606)
			at org.apache.catalina.startup.Catalina.load(Catalina.java:629)
			at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
			at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
			at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
			at java.lang.reflect.Method.invoke(Method.java:498)
			at org.apache.catalina.startup.Bootstrap.load(Bootstrap.java:311)
			at org.apache.catalina.startup.Bootstrap.main(Bootstrap.java:494)
	Caused by: org.apache.catalina.LifecycleException: Protocol handler initialization failed
			at org.apache.catalina.connector.Connector.initInternal(Connector.java:970)
			at org.apache.catalina.util.LifecycleBase.init(LifecycleBase.java:107)
			... 12 more
	Caused by: java.net.BindException: Address already in use
			at sun.nio.ch.Net.bind0(Native Method)
			at sun.nio.ch.Net.bind(Net.java:433)
			at sun.nio.ch.Net.bind(Net.java:425)
			at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
			at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
			at org.apache.tomcat.util.net.NioEndpoint.bind(NioEndpoint.java:210)
			at org.apache.tomcat.util.net.AbstractEndpoint.init(AbstractEndpoint.java:972)
			at org.apache.tomcat.util.net.AbstractJsseEndpoint.init(AbstractJsseEndpoint.java:237)
			at org.apache.coyote.AbstractProtocol.init(AbstractProtocol.java:558)
			at org.apache.catalina.connector.Connector.initInternal(Connector.java:968)
			... 13 more
	```

	- Here we need to see the below lines

	```
	org.apache.catalina.core.StandardService.initInternal Failed to initialize connector [Connector
        [AJP/1.3-8010]]
	Caused by: java.net.BindException: Address already in use
	```
	
	- This tells us that the application is failed to initialize the ***AJP Connector Port*** on ***8010*** as it is addressed already in use
	- Now to fix this let us stop tomcat and change the port back to ***8009*** in the ***$CATALINA_HOME/conf/server.xml***
	- After this start both the instances and can notice that we don't have any issues in either of the instance
