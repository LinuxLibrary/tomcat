# Troubleshooting Tomcat using other log files

- We have already seen how to troubleshoot tomcat instance based on the ***catalina.out*** log
- By default tomcat writes some different logs as defined in the catalina script into the logs directory
- Here we can see some other logs
	- ***localhost.YYYY-MM-DD.log***
		- This log contains information about the server and the application on that server
		- We can see information like ***contextInitialized()*** and ***contextDestroyed()***
		- Everytime we start or stop applications will be logged here as the context Initialized or Destroyed
	- ***localhost_access_log.YYYY-MM-DD.txt***
		- This log contains information about the access from clients to our web application
		- Here we can see each and every action took place while navigating through the client. We can see the activities done through the client.
		- From this log we can log how many users accessing what information.
	- ***host-manager.YYYY-MM-DD.log***
		- This log will say how and when the ***HostManager*** is accessed from the GUI
	- ***manager.YYYY-MM-DD.log***
		- This log will say how and when the ***Manager App*** is accessed from the GUI
