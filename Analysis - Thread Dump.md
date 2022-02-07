# Thread Dump Basics –  
**What is Thread Dump –**  
A thread dump is a snapshot of all the threads of a java application at a certain point in time.

**Why to take ThreadDump –**  
1. When an application seems stuck (due to thread related issues such as deadlocks, etc.)
2. When an application seems to be too slow or almost hanging under high load
3. to optimize application for better performance, or monitor thread level activity

**How to take ThreadDump –**  
1. Using cmd line options - `kill -3 <PID>` on unix machines  
   if, this config is set `-XX:+UnlockDiagnosticVMOptions -XX:+LogVMOutput -XX:LogFile=~/jvm.log`  
   JVM will write the thread dump to /jvm.log file  
2. Ctrl + Break (Windows)  
   If, `Break` key is not available on keyboard, then use Ctrl+Shift+Pause keys in combinations  
3. `jcmd` tool is used to send diagnostic command requests to the JVM, `jcmd <pid> Thread.print > <file-path>`
4. `JVisualVM` - it's a monitoring, troubleshooting tool that is packaged within the JDK,  
5. Using JMX clients such as JConsole, Java Mission Control (using MBeanServer) etc.
6. `jstack` - is a command-line JDK utility to capture a thread dump  
   example: `jstack -l  <pid> > <file-path>`  
7. `jconsole` lets us inspect the stack trace of each thread 
8. and, through programmatic approach like below code snippets - 

```java
import java.io.IOException;
import java.lang.management.ManagementFactory;
import java.lang.management.ThreadInfo;
import java.lang.management.ThreadMXBean;

/**
 * Thread Dump
 *
 */
public class ThreadDump {

	public static void main(String[] args) throws IOException {
		System.out.println("Hello World!");
		ThreadDump app = new ThreadDump();
		app.takeThreadDump();
		int code = System.in.read();
		System.out.println("code: " + code);
	}

	public void takeThreadDump() {
		ThreadMXBean threadMXBean = ManagementFactory.getThreadMXBean();
		for (ThreadInfo ti : threadMXBean.dumpAllThreads(true, true)) {
			System.out.println(ti.toString());
		}
	}
}
```

# Thread Dump Analysis – 

