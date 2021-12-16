# Security Manager - 

A `security manager` is an object that defines a `security policy` for an application.  
This policy specifies actions that are `unsafe` or `sensitive`.  
Any actions not allowed by the security policy cause a `SecurityException` to be thrown.  
An application can also query its security manager to discover which actions are allowed.  

Typically, a `web applet` runs with a security manager provided by the `browser` or Java Web Start plugin.  
Other kinds of applications normally run without a security manager, unless the `application` itself defines one.  
If no `security manager` is present, the `application` has no security policy and acts without restrictions.  

# How to control access to a Java Object:
https://examples.javacodegeeks.com/core-java/security/control-access-to-an-object-example/  

**Reference:**  
1. https://docs.oracle.com/javase/tutorial/essential/environment/security.html
2. https://docs.oracle.com/javase/8/docs/technotes/guides/security/index.html
3. https://www.baeldung.com/java-security-manager
4. https://blog.frankel.ch/java-security-manager/

