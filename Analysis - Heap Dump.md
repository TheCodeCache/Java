# Heap Dump Analysis – 

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
6. and through programmatic approach


