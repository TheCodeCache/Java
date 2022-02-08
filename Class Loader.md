# Why do we need a Custom `ClassLoader` in Java ? 

Java default `ClassLoader` can load classes from the local file system,  
which is good enough for most of the cases.  
But, if you are expecting a class at the runtime  
or from the FTP server  
or via third party web service  
or from URL  
or from database  
or from a file
or from the class created on the fly  
at the time of loading the class,  
then you have to extend the existing class loader.  

For example, AppletViewers load the classes from a remote web server.  

# Class Loader Basics – 

When we compile a Java Class, JVM creates the bytecode, which is platform and machine-independent.  
The bytecode is stored in a `.class` file.  
When we try to use a class, the `ClassLoader` loads it into the memory.  

Every `Class Loader` in JVM is similar to `namespace`, and loads the classes into its own namespace.  
Classes loaded into separate namespace can not interact with each other  

There are three types of built-in ClassLoader in Java –  

1. `Bootstrap` - It loads JDK internal classes, loads rt.jar and other core classes for example java.lang.* package classes.
2. `Extension` - It loads classes from the JDK extensions directory, usually $JAVA_HOME/lib/ext directory.
3. `System` - This classloader loads classes from the current classpath.  
   We can set classpath while invoking a program using -cp or -classpath command line option  

**ClassLoader Hierarchy** –  
When a request is raised to load a class, it delegates it to the parent classloader.  
This is how uniqueness is maintained in the runtime environment.  
If the parent class loader doesn't find the class then the class loader itself tries to load the class.  

Example:  

```java
package com.tests.examples;

public class ClassLoaderTest {
    public static void main(String[] args) {

        System.out.println("class loader for HashMap: " 
                + java.util.HashMap.class.getClassLoader());
        

        System.out.println("class loader for DNSNameService: "
                + sun.net.spi.nameservice.dns.DNSNameService.class.getClassLoader());

        System.out.println("class loader for this class: " 
                + ClassLoaderTest.class.getClassLoader());
    }
}
```

**Output**:  
```java
class loader for HashMap: null
class loader for DNSNameService: sun.misc.Launcher$ExtClassLoader@3d4eac69
class loader for this class: sun.misc.Launcher$AppClassLoader@73d16e93
```

**Explanation**:  

The java.util.HashMap ClassLoader is coming as null, which reflects `Bootstrap ClassLoader`.  
The DNSNameService class ClassLoader is `ExtClassLoader`.  
Since, the class itself is in CLASSPATH, `System ClassLoader` loads it.  

**Loading Mechanism**:  

When we are trying to load HashMap, our System ClassLoader delegates it to the Extension ClassLoader.  
The Extension class loader delegates it to the Bootstrap ClassLoader.  
The bootstrap class loader finds the HashMap class and loads it into the JVM memory.  

The same process is followed for the DNSNameService class.  
But, the Bootstrap ClassLoader is not able to locate it since it's in $JAVA_HOME/lib/ext/dnsns.jar.  
Hence, it gets loaded by Extensions Classloader.  

The classes loaded by a child class loader have visibility into classes loaded by its parent class loaders.  
So, classes loaded by System Classloader have visibility into classes loaded by Extensions and Bootstrap Classloader.  

# Custom ClassLoader – 

```java

```

**Reference:**  
1. https://www.journaldev.com/349/java-classloader

