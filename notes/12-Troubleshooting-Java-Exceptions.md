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
	
