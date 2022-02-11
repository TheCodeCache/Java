# Native Memory Tracking in JVM – 

Let us first understand the commond sources of native memory allocations in JVM  

### 1. Metaspace
In order to maintain some metadata about the loaded classes, The JVM uses a dedicated non-heap area called `Metaspace`  
Before Java 8, the equivalent was called `PermGen` or Permanent Generation.   
`Metaspace` or `PermGen` contains the metadata about the loaded classes rather than the instances of them, which are kept inside the `heap`.  

The heap sizing configurations won't affect the Metaspace size since the Metaspace is an `off-heap` data area  

- `-XX:MetaspaceSize` and `-XX:MaxMetaspaceSize` to set the minimum and maximum Metaspace size
- Before Java 8, `-XX:PermSize` and `-XX:MaxPermSize` to set the minimum and maximum PermGen size

### 2. Threads
One of the most memory-consuming data areas in the JVM is the `stack`, created at the same time as each thread.  
The `stack` stores local variables and partial results, playing an important role in method invocations.  

In contrast with other data areas,  
the total memory allocated to stacks is practically unbounded when there is no limitation on the number of threads  

### 3. Code Cache
When the JVM compiles bytecode to assembly instructions,  
it stores those instructions in a special non-heap data area called `Code Cache`  

The code cache can be managed just like other data areas in the JVM.  
The `-XX:InitialCodeCacheSize` and `-XX:ReservedCodeCacheSize` tuning flags determine the initial and maximum possible size for the code cache  

### 4. Garbage Collection
The JVM is shipped with a handful of GC algorithms, each suitable for different use cases.  
All those GC algorithms share one common trait: they need to use some off-heap data structures to perform their tasks.  
These internal data structures consume more native memory.  

### 5. Symbols
`String` objects usually occupy a large portion of the Heap.  
If a large number of those strings contain the same content, then a significant part of the heap will be wasted  

In order to save some heap space, we can store one version of each String and make others refer to the stored version.  
This process is called String Interning. Since the JVM can only intern Compile Time String Constants,  
we can manually call the intern() method on strings we intend to intern.  

JVM stores interned strings in a special native fixed-sized hashtable called the String Table, also known as the `String Pool`.  
We can configure the table size (i.e. the number of buckets) via the `-XX:StringTableSize` tuning flag.  

In addition to the string table, there's another native data area called the `Runtime Constant Pool`.  
JVM uses this pool to store constants like compile-time numeric literals or method and field references that must be resolved at runtime.  

### 6. Native Byte Buffers
The JVM is the usual suspect for a significant number of native allocations,  
but sometimes developers can directly allocate native memory, too.  
Most common approaches are the malloc call by JNI and NIO's direct `ByteBuffers`.  

### 7. Additional Tuning Flags




**Reference:**  
1. https://www.baeldung.com/native-memory-tracking-in-jvm

