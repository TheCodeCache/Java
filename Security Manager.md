# Security Manager - 

A `security manager` is an object that defines a `security policy` for an application.  
This policy specifies actions that are `unsafe` or `sensitive`.  
Any actions not allowed by the security policy cause a `SecurityException` to be thrown.  
An application can also query its security manager to discover which actions are allowed.  

Typically, a `web applet` runs with a security manager provided by the `browser` or Java Web Start plugin.  
Other kinds of applications normally run without a security manager, unless the `application` itself defines one.  
If no `security manager` is present, the `application` has no security policy and acts without restrictions.  

Actions that are guarded by permissions (in Oracle JDK's security policy) include:  
- Accept a socket connection from a specified host and port number
- Modify a thread (change its priority, stop it, and so on)
- Open a socket connection to a specified host and port number
- Create a new class loader
- Delete a specified file
- Create a new process
- Cause the application to exit
- Load a dynamic library that contains native methods
- Wait for a connection on a specified local port number
- Load a class from a specified package (used by class loaders)
- Add a new class to a specified package (used by class loaders)
- Access or modify system properties
- Access a specified system property
- Read from a specified file
- Write to a specified file

The above are the "really evil things" that an attacker might do,  
However actions that are not guarded are:  
- Allocate memory (this can not be guarded but can be mitigated)  
- Create new threads  
so in this two case, we might have to secure it manually,  

# How to control access to a Java Object:
https://examples.javacodegeeks.com/core-java/security/control-access-to-an-object-example/  

**Reference:**  
1. https://docs.oracle.com/javase/tutorial/essential/environment/security.html
2. https://docs.oracle.com/javase/8/docs/technotes/guides/security/index.html
3. https://www.baeldung.com/java-security-manager
4. https://blog.frankel.ch/java-security-manager/

