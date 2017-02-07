# Tomcat File and Directory Architecture

*Let us know about the directories in ***CATALINA_HOME*** directory*

- ***bin*** In this directory we have all our control scripts / programs / executables of our tomcat application

- ***conf*** In this directory we have all our xml based config files through which we can customize our tomcat application

- ***lib*** In this directory we can have our standard library files. If we want to add any third party libraries then we can drop those here

- ***logs*** All the tomcat logs can be found here.
	- ***localhost*** - Information of Apache Tomcat engine from the host perspective
	- ***manager*** - Information of starting and stopping instances
	- ***host-manager*** - Information about managing Apache tomcat engine
	- ***catalina*** - Logs all the errors in the applications which are running on Tomcat

- ***temp*** - Contains the objects which will cached out to the disk while the engine is running 

- ***webapps*** - Applet contexts or our applications can be found here
	- ***ROOT*** - Here we can place the ***.war*** files of our applications
