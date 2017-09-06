# Customizing a Java Virtual Machine

- Customizing the ***catalina.sh***
	- ***CATALINA_OPTS***

	```
	CATALINA_OPTS="$CATALINA_OPTS $JPDA_OPTS"
	```

	- By default the CATALINA_OPTS line will looks like above. Among which the JPDA_OPTS is used to provide the debug options for the catalina script.
	- Now we need to edit this line and can add our custom options like the size of initial memory of JVM (min. size), the size of memory of the JVM (max. size) it can grow upto, garbage collection options, etc.
	- Add the below at the end of the ***CATALINA_OPTS*** line

	```
	-Xms128m -Xmx256m 
	
	```
	
	- ***-Xms*** means Extended Minimum Size which is the min / initial size of a JVM to start with
	- ***-Xmx*** means Extended Maximum Size which is the max size upto which a JVM can grow
