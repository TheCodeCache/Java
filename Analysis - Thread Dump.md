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

There are several open-sourced analysis tools in the market, the most common tools are listed as follows:  
1. `fast`Thread (https://fastthread.io/)  
2. https://jstack.review/
3. https://spotify.github.io/threaddump-analyzer/
4. JProfiler - it's an standalone tool

**`jstack.review`** :  

<img src="https://user-images.githubusercontent.com/26399543/152868956-244d2cae-2ecc-4854-aa31-ae643f2d26ca.png" width="50%" height="50%">  

**`spotify`** :  

<img src="https://user-images.githubusercontent.com/26399543/152869029-ff6c80e2-2ca6-4935-b59e-1434f472a92b.png" width="50%" height="50%">  

```java
package com.tests.examples;

import java.util.concurrent.Semaphore;

class OddTask implements Runnable {

    private Semaphore oddLock;
    private Semaphore evenLock;

    public OddTask(Semaphore oddLock, Semaphore evenLock) {
        this.oddLock = oddLock;
        this.evenLock = evenLock;
    }

    @Override
    public void run() {
        for (int i = 1; i < 100; i += 2) {
            try {
                oddLock.acquire();
            } catch (Exception e) {
            }
            System.out.println(i + " by odd thread");
            try {
                System.out.println("odd thread sleeping for 5 sec");
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
            evenLock.release();
        }
    }
}

class EvenTask implements Runnable {

    private Semaphore oddLock;
    private Semaphore evenLock;

    public EvenTask(Semaphore oddLock, Semaphore evenLock) {
        this.oddLock = oddLock;
        this.evenLock = evenLock;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i += 2) {
            try {
                evenLock.acquire();
            } catch (InterruptedException e) {
                System.out.println("Intruppted during lock acquisition");
                e.printStackTrace();
            }
            System.out.println(i + " by even thread");
            try {
                System.out.println("even thread sleeping for 5 sec");
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
            oddLock.release();
        }
    }
}

/**
 * Print even and odd numbers using two threads in sequential order manner,
 * while one thread prints only even number and the other thread prints odd number.
 * 
 * @author manoranjan.kumar
 */
public class EvenOdd {

    public static void main(String[] args) {
        System.out.println("begin!");
        Semaphore oddLock = new Semaphore(0);
        Semaphore evenLock = new Semaphore(1);

        Thread odd = new Thread(new OddTask(oddLock, evenLock), "Odd THread");
        Thread even = new Thread(new EvenTask(oddLock, evenLock), "Even THread");

        odd.start();
        even.start();

        try {
            odd.join();
            even.join();
        } catch (InterruptedException e) {
            System.out.println("Intruppted while joining threads");
            e.printStackTrace();
        }
        System.out.println("main exits now!");
    }
}
```

PFB for 3 thread-dump files taken at the interval of 10 seconds each upon execution of above code –  

- [thread-dump1.log](https://github.com/TheCodeCache/Java/files/8018809/thread-dump1.log)  
- [thread-dump2.log](https://github.com/TheCodeCache/Java/files/8018810/thread-dump2.log)  
- [thread-dump3.log](https://github.com/TheCodeCache/Java/files/8018812/thread-dump3.log)  

Let us analyze these using `fastThread` tool  

just open up https://fastthread.io/  

![image](https://user-images.githubusercontent.com/26399543/152874111-4fb67b15-33df-443d-ac8f-bb902ae402ad.png)  
![image](https://user-images.githubusercontent.com/26399543/152874054-2507b18e-8f34-437b-ac8f-dab1ff5c3731.png)  

Attach the thread-dump file (thread-dump1.log)  

and PFB the results –  

https://fastthread.io/my-thread-report.jsp?p=c2hhcmVkLzIwMjIvMDIvNy8tLXRocmVhZC1kdW1wMS5sb2ctLTIxLTE5LTEw&

OR, in PDF format –  

[Report-thread-dump1.pdf](https://github.com/TheCodeCache/Java/files/8018865/ft-report-thread-dump1.pdf)

