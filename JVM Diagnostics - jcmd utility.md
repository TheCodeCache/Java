# `jcmd` utility to probe into JVM – 

The **`jcmd`** utility is used to send diagnostic command requests to the JVM  
These requests are useful for controlling `Java Flight Recordings`, `troubleshoot`, and `diagnose JVM` and `Java Applications`  
It must be used on the same machine where the JVM is running,  
and have the same effective user and group identifiers that were used to launch the JVM.  

A special command **`jcmd <process id/main class> PerfCounter.print`** prints all performance counters in the process.  

```java
C:\Users\manoranjan.kumar>jcmd 17652 PerfCounter.print
17652:
java.ci.totalTime=9823
java.cls.loadedClasses=413
java.cls.sharedLoadedClasses=0
java.cls.sharedUnloadedClasses=0
java.cls.unloadedClasses=0
java.property.java.class.path="D:\samples\code-coverage\target\classes"
java.property.java.endorsed.dirs="C:\Program Files\Java\jdk1.8.0_121\jre\lib\endorsed"
java.property.java.ext.dirs="C:\Program Files\Java\jdk1.8.0_121\jre\lib\ext;C:\Windows\Sun\Java\lib\ext"
java.property.java.home="C:\Program Files\Java\jdk1.8.0_121\jre"
java.property.java.library.path="C:\Program Files\Java\jdk1.8.0_121\bin;C:\Windows\Sun\Java\bin;C:\Windows\system32;C:\Windows;D:/tools/jeclipse//plugins/org.eclipse.justj.openjdk.hotspot.jre.full.win32.x86_64_16.0.2.v20210721-1149/jre/bin/server;D:/tools/jeclipse//plugins/org.eclipse.justj.openjdk.hotspot.jre.full.win32.x86_64_16.0.2.v20210721-1149/jre/bin;C:\Program Files\Python39\Scripts\;C:\Program Files\Python39\;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\PuTTY\;C:\Program Files\TortoiseGit\bin;C:\Program Files\Java\jdk1.8.0_121\bin;C:\Program Files\Python39\Scripts\;C:\Program Files\Python39\Lib\;C:\Program Files\Python39\;C:\Program Files\Python39\Scripts\;C:\Program Files\Python39\;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\PuTTY\;C:\Program Files\TortoiseGit\bin;C:\Program Files\Java\jdk1.8.0_121\bin;C:\Program Files\Python39\Scri"
java.property.java.version="1.8.0_121"
java.property.java.vm.info="mixed mode"
java.property.java.vm.name="Java HotSpot(TM) 64-Bit Server VM"
java.property.java.vm.specification.name="Java Virtual Machine Specification"
java.property.java.vm.specification.vendor="Oracle Corporation"
java.property.java.vm.specification.version="1.8"
java.property.java.vm.vendor="Oracle Corporation"
java.property.java.vm.version="25.121-b13"
java.rt.vmArgs="-XX:NativeMemoryTracking=summary -Xms300m -Xmx300m -XX:+UseG1GC -Dfile.encoding=UTF-8 -Xbootclasspath:C:\Program Files\Java\jdk1.8.0_121\jre\lib\resources.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\rt.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\jsse.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\jce.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\charsets.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\jfr.jar;C:\Program Files\Java\jdk1.8.0_121\lib\tools.jar;D:\jars\jna-3.5.1.jar;D:\jars\jna-platform-4.0.0.jar"
java.rt.vmFlags=""
java.threads.daemon=4
java.threads.live=5
java.threads.livePeak=5
java.threads.started=5
sun.ci.compilerThread.0.compiles=1
sun.ci.compilerThread.0.method=""
sun.ci.compilerThread.0.time=0
sun.ci.compilerThread.0.type=1
sun.ci.compilerThread.1.compiles=0
sun.ci.compilerThread.1.method=""
sun.ci.compilerThread.1.time=0
sun.ci.compilerThread.1.type=0
sun.ci.compilerThread.2.compiles=0
sun.ci.compilerThread.2.method=""
sun.ci.compilerThread.2.time=0
sun.ci.compilerThread.2.type=0
sun.ci.compilerThread.3.compiles=25
sun.ci.compilerThread.3.method=""
sun.ci.compilerThread.3.time=3
sun.ci.compilerThread.3.type=1
sun.ci.lastFailedMethod=""
sun.ci.lastFailedType=0
sun.ci.lastInvalidatedMethod=""
sun.ci.lastInvalidatedType=0
sun.ci.lastMethod="java/lang/StringBuilder append"
sun.ci.lastSize=8
sun.ci.lastType=1
sun.ci.nmethodCodeSize=20128
sun.ci.nmethodSize=33488
sun.ci.osrBytes=0
sun.ci.osrCompiles=0
sun.ci.osrTime=0
sun.ci.standardBytes=1326
sun.ci.standardCompiles=26
sun.ci.standardTime=9823
sun.ci.threads=4
sun.ci.totalBailouts=0
sun.ci.totalCompiles=26
sun.ci.totalInvalidates=0
sun.classloader.findClassTime=6230357
sun.classloader.findClasses=1
sun.classloader.parentDelegationTime=9181551
sun.cls.appClassBytes=1725
sun.cls.appClassLoadCount=9
sun.cls.appClassLoadTime=173
sun.cls.appClassLoadTime.self=173
sun.cls.classInitTime=68955
sun.cls.classInitTime.self=40657
sun.cls.classLinkedTime=12344
sun.cls.classLinkedTime.self=10893
sun.cls.classVerifyTime=1416
sun.cls.classVerifyTime.self=1325
sun.cls.defineAppClassTime=227
sun.cls.defineAppClassTime.self=13
sun.cls.defineAppClasses=1
sun.cls.initializedClasses=333
sun.cls.isUnsyncloadClassSet=0
sun.cls.jniDefineClassNoLockCalls=0
sun.cls.jvmDefineClassNoLockCalls=1
sun.cls.jvmFindLoadedClassNoLockCalls=20
sun.cls.linkedClasses=369
sun.cls.loadInstanceClassFailRate=0
sun.cls.loadedBytes=863040
sun.cls.lookupSysClassTime=37606
sun.cls.methodBytes=598384
sun.cls.nonSystemLoaderLockContentionRate=0
sun.cls.parseClassTime=31084
sun.cls.parseClassTime.self=27213
sun.cls.sharedClassLoadTime=12
sun.cls.sharedLoadedBytes=0
sun.cls.sharedUnloadedBytes=0
sun.cls.sysClassBytes=1613601
sun.cls.sysClassLoadTime=78136
sun.cls.systemLoaderLockContentionRate=0
sun.cls.time=117830
sun.cls.unloadedBytes=0
sun.cls.unsafeDefineClassCalls=0
sun.cls.verifiedClasses=369
sun.gc.cause="No GC"
sun.gc.collector.0.invocations=0
sun.gc.collector.0.lastEntryTime=0
sun.gc.collector.0.lastExitTime=0
sun.gc.collector.0.name="G1 incremental collections"
sun.gc.collector.0.time=0
sun.gc.collector.1.invocations=0
sun.gc.collector.1.lastEntryTime=0
sun.gc.collector.1.lastExitTime=0
sun.gc.collector.1.name="G1 stop-the-world full collections"
sun.gc.collector.1.time=0
sun.gc.compressedclassspace.capacity=393216
sun.gc.compressedclassspace.maxCapacity=1073741824
sun.gc.compressedclassspace.minCapacity=0
sun.gc.compressedclassspace.used=77688
sun.gc.generation.0.agetable.bytes.00=0
sun.gc.generation.0.agetable.bytes.01=0
sun.gc.generation.0.agetable.bytes.02=0
sun.gc.generation.0.agetable.bytes.03=0
sun.gc.generation.0.agetable.bytes.04=0
sun.gc.generation.0.agetable.bytes.05=0
sun.gc.generation.0.agetable.bytes.06=0
sun.gc.generation.0.agetable.bytes.07=0
sun.gc.generation.0.agetable.bytes.08=0
sun.gc.generation.0.agetable.bytes.09=0
sun.gc.generation.0.agetable.bytes.10=0
sun.gc.generation.0.agetable.bytes.11=0
sun.gc.generation.0.agetable.bytes.12=0
sun.gc.generation.0.agetable.bytes.13=0
sun.gc.generation.0.agetable.bytes.14=0
sun.gc.generation.0.agetable.bytes.15=0
sun.gc.generation.0.agetable.size=16
sun.gc.generation.0.capacity=16777240
sun.gc.generation.0.maxCapacity=314572824
sun.gc.generation.0.minCapacity=24
sun.gc.generation.0.name="young"
sun.gc.generation.0.space.0.capacity=16777224
sun.gc.generation.0.space.0.initCapacity=16777224
sun.gc.generation.0.space.0.maxCapacity=314572808
sun.gc.generation.0.space.0.name="eden"
sun.gc.generation.0.space.0.used=0
sun.gc.generation.0.space.1.capacity=8
sun.gc.generation.0.space.1.initCapacity=8
sun.gc.generation.0.space.1.maxCapacity=8
sun.gc.generation.0.space.1.name="s0"
sun.gc.generation.0.space.1.used=0
sun.gc.generation.0.space.2.capacity=8
sun.gc.generation.0.space.2.initCapacity=8
sun.gc.generation.0.space.2.maxCapacity=314572808
sun.gc.generation.0.space.2.name="s1"
sun.gc.generation.0.space.2.used=0
sun.gc.generation.0.spaces=3
sun.gc.generation.1.capacity=297795592
sun.gc.generation.1.maxCapacity=314572808
sun.gc.generation.1.minCapacity=8
sun.gc.generation.1.name="old"
sun.gc.generation.1.space.0.capacity=297795592
sun.gc.generation.1.space.0.initCapacity=297795592
sun.gc.generation.1.space.0.maxCapacity=314572808
sun.gc.generation.1.space.0.name="space"
sun.gc.generation.1.space.0.used=0
sun.gc.generation.1.spaces=1
sun.gc.lastCause="No GC"
sun.gc.metaspace.capacity=4587520
sun.gc.metaspace.maxCapacity=1082130432
sun.gc.metaspace.minCapacity=0
sun.gc.metaspace.used=788776
sun.gc.policy.collectors=1
sun.gc.policy.desiredSurvivorSize=0
sun.gc.policy.generations=3
sun.gc.policy.maxTenuringThreshold=15
sun.gc.policy.name="GarbageFirst"
sun.gc.policy.tenuringThreshold=15
sun.gc.tlab.alloc=0
sun.gc.tlab.allocThreads=0
sun.gc.tlab.fastWaste=0
sun.gc.tlab.fills=0
sun.gc.tlab.gcWaste=0
sun.gc.tlab.maxFastWaste=0
sun.gc.tlab.maxFills=0
sun.gc.tlab.maxGcWaste=0
sun.gc.tlab.maxSlowAlloc=0
sun.gc.tlab.maxSlowWaste=0
sun.gc.tlab.slowAlloc=0
sun.gc.tlab.slowWaste=0
sun.os.hrt.frequency=1945314
sun.os.hrt.ticks=29972930
sun.perfdata.majorVersion=2
sun.perfdata.minorVersion=0
sun.perfdata.overflow=0
sun.perfdata.size=65536
sun.perfdata.timestamp=238096
sun.perfdata.used=17176
sun.property.sun.boot.class.path="C:\Program Files\Java\jdk1.8.0_121\jre\lib\resources.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\rt.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\jsse.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\jce.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\charsets.jar;C:\Program Files\Java\jdk1.8.0_121\jre\lib\jfr.jar;C:\Program Files\Java\jdk1.8.0_121\lib\tools.jar;D:\jars\jna-3.5.1.jar;D:\jars\jna-platform-4.0.0.jar"
sun.property.sun.boot.library.path="C:\Program Files\Java\jdk1.8.0_121\jre\bin"
sun.rt._sync_ContendedLockAttempts=0
sun.rt._sync_Deflations=3
sun.rt._sync_EmptyNotifications=0
sun.rt._sync_FailedSpins=0
sun.rt._sync_FutileWakeups=0
sun.rt._sync_Inflations=5
sun.rt._sync_MonExtant=128
sun.rt._sync_MonInCirculation=0
sun.rt._sync_MonScavenged=0
sun.rt._sync_Notifications=2
sun.rt._sync_Parks=2
sun.rt._sync_PrivateA=0
sun.rt._sync_PrivateB=0
sun.rt._sync_SlowEnter=0
sun.rt._sync_SlowExit=0
sun.rt._sync_SlowNotify=0
sun.rt._sync_SlowNotifyAll=0
sun.rt._sync_SuccessfulSpins=0
sun.rt.applicationTime=7871683
sun.rt.createVmBeginTime=1644641960869
sun.rt.createVmEndTime=1644641960977
sun.rt.internalVersion="Java HotSpot(TM) 64-Bit Server VM (25.121-b13) for windows-amd64 JRE (1.8.0_121-b13), built on Dec 12 2016 18:21:36 by "java_re" with MS VC++ 10.0 (VS2010)"
sun.rt.interruptedBeforeIO=0
sun.rt.interruptedDuringIO=0
sun.rt.javaCommand="com.thecodecache.code_coverage.App"
sun.rt.jvmCapabilities="1100000000000000000000000000000000000000000000000000000000000000"
sun.rt.jvmVersion=427360269
sun.rt.safepointSyncTime=914
sun.rt.safepointTime=1346
sun.rt.safepoints=2
sun.rt.threadInterruptSignaled=0
sun.rt.vmInitDoneTime=1644641960936
sun.threads.vmOperationTime=82
sun.urlClassLoader.readClassBytesTime=2427886
sun.zip.zipFile.openTime=0
sun.zip.zipFiles=0
```

The command jcmd <process id/main class> <command> [options] sends the actual command to the JVM.  

### 1. Diagnostic Command Request using `jcmd` utility
```
C:\Users\manoranjan.kumar>jps -l
32852 sun.tools.jps.Jps
13352 com.thecodecache.code_coverage.App
21864 Eclipse

C:\Users\manoranjan.kumar>jcmd
21864 Eclipse
32936 com.thecodecache.code_coverage.App
19164 sun.tools.jcmd.JCmd

C:\Users\manoranjan.kumar>jcmd 13352 help
13352:
The following commands are available:
JFR.stop
JFR.start
JFR.dump
JFR.check
VM.native_memory
VM.check_commercial_features
VM.unlock_commercial_features
ManagementAgent.stop
ManagementAgent.start_local
ManagementAgent.start
GC.rotate_log
Thread.print
GC.class_stats
GC.class_histogram
GC.heap_dump
GC.run_finalization
GC.run
VM.uptime
VM.flags
VM.system_properties
VM.command_line
VM.version
help

For more information about a specific command use 'help <command>'.
```

### 2. Useful Commands for jcmd Utility
The available diagnostic command may be different in different versions of HotSpot VM  

1. **Print full HotSpot and JDK version ID** –  
```
jcmd <process id/main class> VM.version
```
2. **Print all the system properties set for a VM**–
```
jcmd <process id/main class> VM.system_properties
```
3. **Print all the flags used for a VM**–
```
jcmd <process id/main class> VM.flags
```
4. **Print the uptime in seconds**–
```
jcmd <process id/main class> VM.uptime
```
5. **Create a class histogram**–
Classes taking the most memory are listed at the top, and classes are listed in a descending order.  
```
jcmd <process id/main class> GC.class_histogram
```
6. **Create a heap dump (hprof dump)**–
```
jcmd GC.heap_dump filename=Myheapdump
```
   this is same as  
```
jmap -dump:file=<file> <pid>
```
   but `jcmd` is the recommended tool to use  
7. **Create a heap histogram**–
```
jcmd <process id/main class> GC.class_histogram filename=Myheaphistogram
```
This is the same as using `jmap -histo <pid>`, but `jcmd` is the recommended tool to use.
8. **Print all threads with stack traces**–
```
jcmd <process id/main class> Thread.print
```

### 3. Troubleshoot with jcmd Utility
The jcmd utility provides the following troubleshooting options:  

1. **Start a flight recording**–
2. 
**For example–** To start a 2-minute recording on the running Java process with the identifier 7060  
and save it to myrecording.jfr in the current directory, use the following:  
```
jcmd 7060 JFR.start name=MyRecording settings=profile delay=20s duration=2m filename=C:\TEMP\myrecording.jfr
```
2. **Check a recording**–
   The JFR.check diagnostic command checks a running recording. For example:  
```
jcmd 7060 JFR.check
```
3. **Stop a recording**–
The JFR.stop diagnostic command stops a running recording and has the option to discard the recording data. For example:  
```
jcmd 7060 JFR.stop
```
4. **Dump a recording**–
The JFR.dump diagnostic command stops a running recording and has the option to dump recordings to a file. For example:  
```
jcmd 7060 JFR.dump name=MyRecording filename=C:\TEMP\myrecording.jfr
```
5. **Create a heap dump**–
The preferred way to create heap dump is:  
```
jcmd <pid> GC.heap_dump filename=Myheapdump
```
6. **Create a heap histogram**–
The preferred way to create a heap histogram is  
```
jcmd <pid> GC.class_histogram filename=Myheaphistogram
```

**Reference:**  
1. https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr006.html

