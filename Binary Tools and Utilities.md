# JDK Tools and Utilities – 

**Basic Tools** –  
1. `java` - The launcher for Java applications
2. `javac` - The compiler for the Java programming language
3. `javadoc` - API documentation generator  
   In Eclipse IDE, Navigate to `Project` menu, and click `Generate Javadoc` to a target folder.  
   this'll generate the javadoc, look for index.html, open it in web-browser, and we can see the documents generated,  
   we can host the same on web server or roll-out to clients if required
4. `javah` - C header and stub generator. Used to write native methods
5. `javap` - Class file disassembler  
   This gives us the `structure of a java program` (either user program or JDK classes like String, Object etc)
   ![image](https://user-images.githubusercontent.com/26399543/153005800-8ee2f8ca-d073-4b8d-9bea-006da43930e6.png)  
6. `jdp` - The Java Debugger
7. `jdeps` - Java class dependency analyzer  
   ![image](https://user-images.githubusercontent.com/26399543/153006218-50127da3-dc2a-433d-be8b-bc55443b8c36.png)  

**Java Troubleshooting, Profiling, Monitoring and Management Tools** –  
1. `jcmd` - JVM Diagnostic Commands tool - Sends diagnostic command requests to a running Java Virtual Machine
2. `jconsole` - A JMX-compliant graphical tool for monitoring a Java virtual machine.  
   It can monitor both local and remote JVMs  
3. `jmc` - The `Java Mission Control` (JMC) client includes tools to monitor and manage your Java application  
   without introducing the performance overhead normally associated with these types of tools.  
4. `jvisualvm` - A graphical tool that provides detailed information about the Java technology-based applications,  
   while they are running in a Java Virtual Machine.  
   Java VisualVM provides memory and CPU profiling, heap dump analysis, memory leak detection, access to MBeans,  
   and garbage collection

**Monitoring Tools** –  
1. `jps` - Experimental: JVM Process Status Tool - Lists instrumented HotSpot Java virtual machines on a target system  
2. `jstat` - Experimental: JVM Statistics Monitoring Tool - Attaches to an instrumented HotSpot Java virtual machine  
   and collects and logs performance statistics as specified by the command line options.  
3. `jstatd` - Experimental: JVM jstat Daemon - Launches an RMI server application that monitors for the creation and  
   termination of instrumented HotSpot Java virtual machines and provides a interface to allow remote monitoring tools  
   to attach to Java virtual machines running on the local system

**Troubleshooting Tools** –  
1. `jhat` - Experimental - Heap Dump Browser - Starts a web server on a heap dump file  
   (for example, produced by jmap -dump), allowing the heap to be browsed.  
2. `jmap` - Experimental - Memory Map for Java - Prints shared object memory maps or heap memory details  
   of a given process or core file or a remote debug server.  
3. `jstack` - Experimental - Stack Trace for Java - Prints a stack trace of threads  
   for a given process or core file or remote debug server.  


**Reference:**  
1. https://docs.oracle.com/javase/8/docs/technotes/tools/

