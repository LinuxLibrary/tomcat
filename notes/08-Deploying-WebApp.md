# Deploying Web Application on Tomcat

- For deploying a web application oon tomcat we should have ***.war*** file of the application
- Once we have the ***.war*** file then we need to put it in ***webapps*** directory
- After copying the ***.war*** file restart tomcat
- Another way of deploying application on tomcat is through the Manager GUI
- Go to the deploy section 
- Browse and select your application 
- Click on ***Deploy***
- Now to use your application you need to use your url like below

```
http://< IP / HOSTNAME of Tomcat >:<PORT>/<APPLICATION_NAME_WITHOUT_WAR EXTENSION>

Ex:

http://dev02.linux-library.com:8080/jenkins
```
- 
