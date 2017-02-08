# Security and User Accounts

- If we need to access the Tomcat WebApplications then we need to setup some user accounts.
- For this we need to edit the ***conf/tomcat-users.xml*** 
- At the bottom of this file we can find some roles and user accounts
- Let us add some new roles and users now
	- Adding ***manager, manager-gui, admin-gui*** roles
	
	```
	<role rolename="tomcat"/>
	<role rolename="manager"/>
	<role rolename="manager-gui"/>
	<role rolename="admin-gui"/>
	```
	
	- Adding ***admintom*** user
	
	```
	<user username="admintom" password="s3cret" roles="manager,manager-gui,admin-gui"/>
	```

- Now setting up your Hostname / IP to your server instead of localhost
	- Open ***conf/server.xml*** and edit the following lines to add your Hostname

	```
	Find the line starts with Engine and change the value of defaultHost
	<Engine name="Catalina" defaultHost="dev02.linux-library.com">
	
	Find the line starts with Host change the value of name to your hostname same as above
	<Host name="dev02.linux-library.com"  appBase="webapps"
	```

- If you want to access the tomcat manager from other than your local machine then you need to allow those IP ranges
	- To allow IPs to access manager edit ***webapps/manager/META-INF/context.xml*** file

	> NOTE: If you want to access the app from a host of Class-A IP then you should add 10\.\d+\.\d+\.\d+ to the allow directive
	> That should look like below. I have allowed Class-A as well as Class-C ranges

	```
	allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1|10\.\d+\.\d+\.\d+|192\.168\.1\.\d+" />
	```

	- In the same way you can allow access to you hostmanager too.
	- Open ***webapps/host-manager/META-INF/context.xml*** and edit same as above
