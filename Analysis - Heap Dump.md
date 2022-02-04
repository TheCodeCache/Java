# Heap Dump Basics – 

**What is Heap Dump** –  
A heap dump is a snapshot of the memory of a java application at a certain point in time.  
Since it's just a snapshot, hence it does not contain information such as when and where (in which method) an object was allocated  

**Why to take Heap Dump** –  
1. when a system crashed periodically due to `OOM error`
2. To analyze the `memory footprint of an application`
3. To know the root cause behind `too many garbage objects` being created

**Types of HeapDump** –  
1. `.hprof` binary heap dumps -  
  it contains informations about `all loaded classes` and `all objects`, a list of `gc roots` and `callstacks of all threads`  
2. IBM system dumps 
3. IBM portable heap dumps

**How to take HeapDump** –  
1. Usig cmd line options - 
  `jmap -dump:live,format=b,file=<file-path> <pid>`  
  where <pid> is the java process id for which heap dump should be captured  
  `live` option will only capture live objects on heap, this reduces the size of heap dump & make analysis easier  
  `jmap` is a tool to print statistics about memory in a running JVM. We can use it for local or remote processes 
2. `HeapDumpOnOutOfMemoryError`  
  `-XX:+HeapDumpOnOutOfMemoryError -XX:+HeapDumpPath=/opt/tmp/heapdump.bin`  
3. `jcmd` tool is used to send diagnostic command requests to the JVM, 
  `jcmd <pid> GC.heap_dump file=<file=path>` 
4. `JVisualVM` - it's a monitoring, troubleshooting tool that is packaged within the JDK, 
  when we launch this tool, it'll displays all the running java processes on local machine, and can connect to them 
5. Using JMX clients such as JConsole, Java Mission Control (using MBeanServer) etc.
6. Using `jhat` cmd tool
6. and, through programmatic approach like below code snippets - 
```java
package com.tests.examples;

import java.io.IOException;
import java.lang.management.ManagementFactory;

import javax.management.MBeanServer;

import com.sun.management.HotSpotDiagnosticMXBean;

/**
 * @author manoranjan.kumar
 */
public class HeapDump {
	private static final String HOTSPOT_BEAN_NAME = "com.sun.management:type=HotSpotDiagnostic";

	// available in java 11
	private static volatile HotSpotDiagnosticMXBean hotSpotDiagnosticMXBean;

	public static void main(String[] args) throws IOException {
		HeapDump heapDump = new HeapDump();
		heapDump.takeHeapDump("log_heap_dump.hprof", true);
	}

	public void takeHeapDump(String fileName, boolean live) throws IOException {
		initHotSpotMBean();
		hotSpotDiagnosticMXBean.dumpHeap(fileName, live);
	}

	private static void initHotSpotMBean() throws IOException {
		if (hotSpotDiagnosticMXBean == null) {
			synchronized (HeapDump.class) {
				hotSpotDiagnosticMXBean = getHotSpotDiagnosticMXBean();
			}
		}
	}

	private static HotSpotDiagnosticMXBean getHotSpotDiagnosticMXBean() throws IOException {
		MBeanServer server = ManagementFactory.getPlatformMBeanServer();
		return ManagementFactory.newPlatformMXBeanProxy(server, HOTSPOT_BEAN_NAME, HotSpotDiagnosticMXBean.class);
	}
}
```

# Heap Dump Analysis – 

There are several open-sourced analysis tools in the market, the most common tools are listed as follows:  
1. Eclipse MAT: it comes in two versions - `Standalone` and `Eclipse plug-in`, better use `standalone` version
2. HeapHero:
3. JVisualVM: 

**Eclipse MAT (memory analyzer tool) -**  
download link: [this](https://www.eclipse.org/downloads/download.php?file=/mat/1.12.0/rcp/MemoryAnalyzer-1.12.0.20210602-win32.win32.x86_64.zip)  

code to be analyzed for memory hogging:  
```java
package com.tests.examples;

import java.util.HashMap;
import java.util.Map;

/**
 * Replicating OOM Error Scenario
 * 
 * @author manoranjan.kumar
 */
public class OutOfMemoryError {

	private Map<Object, Object> myMap = new HashMap<>();

	public static void main(String[] args) {
		OutOfMemoryError oom = new OutOfMemoryError();
		oom.grow();
	}

	public void grow() {
		try {
			long counter = 0;
			while (true) {
				myMap.put("key" + counter,
						"Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String "
								+ "Large String Large String Large String Large String Large String " + counter);
				++counter;
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
}
```
  
Compile and Run the above code with these JVM flags:  
`java OutOfMemoryError -Xmx1024m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=java_heap_space_oom_heap_dump.bin`  

it'll throw below error in standard console-  
```java
java.lang.OutOfMemoryError: Java heap space
Dumping heap to java_heap_space_oom_heap_dump.bin ...
Heap dump file created [851946015 bytes in 2.321 secs]
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at java.util.Arrays.copyOfRange(Arrays.java:3664)
	at java.lang.String.<init>(String.java:207)
	at java.lang.StringBuilder.toString(StringBuilder.java:407)
	at com.tests.examples.OutOfMemoryError.grow(OutOfMemoryError.java:25)
	at com.tests.examples.OutOfMemoryError.main(OutOfMemoryError.java:17)
```

Open up this file (java_heap_space_oom_heap_dump.bin) in Eclipse MAT tool, like below  

![image](https://user-images.githubusercontent.com/26399543/152468289-d115b684-81f9-4389-8bba-ddbedfd85b0d.png)  

click on `Dominator Tree` hyper link -  
and then expand the first line item having the maximum `Retained Heap`  
![image](https://user-images.githubusercontent.com/26399543/152468545-4501b4ac-5762-48ca-946b-095bbfd36334.png)  

We can clearly notice the higlighted user-defined class name with complete package details which is having highest `Retained Heap`  

Do, right click on it, like below   
![image](https://user-images.githubusercontent.com/26399543/152468693-e58395dd-3be6-4fbd-b8b4-3233d0ddd2c7.png)  

Expand it, and we can pinpoint the exact varible `myMap` which is causing memory hog as follows-  
![image](https://user-images.githubusercontent.com/26399543/152468758-7997ce33-51e9-45ce-9fd2-ee393dc7b703.png)  

**Shallow Heap:**  
It is the amount of memory occupied by that particular object on Heap.  
**Retained Heap:**  
It is the amount of memory that can be collected by GC when a particular object is removed from Heap  

The below diagram explains Shallow & Retained Heap concepts clearly:  
![image](https://user-images.githubusercontent.com/26399543/152469709-977e48f8-bd27-454c-8410-96270353afa4.png)  


# Heap Dump Analysis using `jhat` -  
For a quick summary, we can using `jhat` to analyze heap dumps, but this is mostly in textual format,  
hence, it may not be that readable, better use UI based tools  
such as, JVisualVM or Eclipse MAT for easier understanding with more features  

![image](https://user-images.githubusercontent.com/26399543/152470491-45d4979c-ad05-4bb0-bd8e-b7d626b9b62d.png)  

open up the browser and hit `localhost:7000`  
![image](https://user-images.githubusercontent.com/26399543/152470595-2253a4b5-0d05-4c9c-8c1d-18665891439e.png)  

	

**Reference:**  
1. https://www.youtube.com/watch?v=gfOdYLVVTFs
2. https://www.youtube.com/watch?v=SuguH8YBl5g

