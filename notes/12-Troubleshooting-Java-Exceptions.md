# Troubleshooting Common Java Exceptions

- Below is an example of ***NullPointer*** Exception

	```
	Exception in thread "main" java.lang.NullPointerException
		at com.example.myproject.Object1.getValue(Object1.java:16)
		at com.example.myproject.Object2.getNumericValue(Object2.java:25)
		at com.example.myproject.Object3.main(Object3.java:14)
	```
	
	- In this case we need to navigate to the file ***Object1*** and review the method called ***getValue()*** to determine what happened
	- The remaining lines give the further information about how the exception was arrived at.
	
- Most of the times we'll have something different to the above, but the above given can be taken as a basic example of how to find out the issue.
- Let us look at the below log once

	```
	Exception in thread "main" java.lang.NullPointerException
		at com.example.myproject.Object1.getValue(Object1.java:16)
		at com.example.myproject.Object2.getNumericValue(Object2.java:25)
		at com.example.myproject.Object3.main(Object3.java:14)
	Caused by: java.lang.IllegalReferenceException
		at com.example.myproject.Object1.getParentValue(Object1.java:22)
	```

	- This means that we have a ***NullPointer*** exception in ***Object1*** at the ***getValue()*** method occured as ***Object1*** and ***getParentValue()*** method thrown a ***IllegalReferenceException*** and this is the initial cause of the problem.
	- If we have multiple ***Caused by*** sections then the lowest is the initial cause of the problem.
