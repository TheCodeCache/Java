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
java -XX:+PrintFlagsFinal -version | grep Metaspace
. . . 
uintx **MetaspaceSize**                             = 21807104                            {pd product}
uintx **MaxMetaspaceSize**                          = 4294901760                          {product}
. . . 

# Native Memory Tracking (NMT)
Now that we know the common sources of native memory allocations in the JVM,  
let us find out how to monitor them  

**Enable** the `native memory tracking` using yet another JVM tuning flag: `-XX:NativeMemoryTracking`=**off**|**sumary**|**detail**  

```java
java -XX:NativeMemoryTracking=summary -Xms300m -Xmx300m -XX:+UseG1GC -jar app.jar
```
Here, we're enabling the NMT while allocating 300 MB of heap space, with G1 as our GC algorithm.  

### 1. Instant Snapshots
We can use **`jcmd`** commandto get details on native memory usage when NMT is turned on  

```
jcmd <pid> VM.native_memory
```
Run any hello world java program, make sure we use Thread.sleep(30000) for 30 seconds,  
so that should be enough for us to get the process-id i.e. PID and run `jcmd` command  
**For ex:**  

```java
/**
 * Class under Native Memory Tracking
 * 
 * @author manoranjan.kumar
 */
public class App {

	public boolean isPalindrome(String input) {

		if (input == null) {
			throw new IllegalArgumentException("input shouldn't be null");
		}
		if (input.equals(reverse(input))) {
			return true;
		}

		return false;
	}

	/**
	 * just for the illustration purpose
	 * 
	 * just a plain simple function, not a sophisticated one,
	 * 
	 * @param input
	 * @return
	 */
	private String reverse(String input) {
		String reverse = "";
		for (int i = input.length() - 1; i >= 0; i--) {
			reverse += input.charAt(i);
		}
		return reverse;
	}

	public static void main(String[] args) {
		System.out.println("Hello World!");
		App app = new App();
		System.out.println(app.isPalindrome("malayalam"));
		try {
			Thread.sleep(30000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
}
```

Run the above program:  
```
java -XX:NativeMemoryTracking=summary -Xms300m -Xmx300m -XX:+UseG1GC App.java
```

Open up command prompt and run this `jps -l` to get the process-id  
```
C:\Users\manoranjan.kumar>jps -l
21864 Eclipse
32840 sun.tools.jps.Jps
11580 com.thecodecache.code_coverage.App
```

**Output:**  
```
C:\Users\manoranjan.kumar>jcmd 11580 VM.native_memory
11580:

Native Memory Tracking:

Total: reserved=1712794KB, committed=413186KB
-                 Java Heap (reserved=307200KB, committed=307200KB)
                            (mmap: reserved=307200KB, committed=307200KB)

-                     Class (reserved=1056893KB, committed=4989KB)
                            (classes #413)
                            (malloc=125KB #167)
                            (mmap: reserved=1056768KB, committed=4864KB)

-                    Thread (reserved=33926KB, committed=33926KB)
                            (thread #34)
                            (stack: reserved=33792KB, committed=33792KB)
                            (malloc=95KB #178)
                            (arena=39KB #66)

-                      Code (reserved=249638KB, committed=2574KB)
                            (malloc=38KB #313)
                            (mmap: reserved=249600KB, committed=2536KB)

-                        GC (reserved=61731KB, committed=61731KB)
                            (malloc=17443KB #2019)
                            (mmap: reserved=44288KB, committed=44288KB)

-                  Compiler (reserved=133KB, committed=133KB)
                            (malloc=2KB #25)
                            (arena=131KB #3)

-                  Internal (reserved=1010KB, committed=1010KB)
                            (malloc=946KB #1827)
                            (mmap: reserved=64KB, committed=64KB)

-                    Symbol (reserved=1366KB, committed=1366KB)
                            (malloc=911KB #99)
                            (arena=456KB #1)

-    Native Memory Tracking (reserved=80KB, committed=80KB)
                            (malloc=5KB #58)
                            (tracking overhead=75KB)

-               Arena Chunk (reserved=176KB, committed=176KB)
                            (malloc=176KB)

-                   Unknown (reserved=640KB, committed=0KB)
                            (mmap: reserved=640KB, committed=0KB)
```

Let's analyze the NMT output section by section.  

### 2. Total Allocations
NMT reports the total reserved and committed memory as follows:  
Total: reserved=1712794KB, committed=413186KB  

Despite allocating 300 MB of heap, the total reserved memory for our app is almost 1.7 GB,  
much more than that. Similarly, the committed memory is around 440 MB, which is, again, much more than that 300 MB.  

`Reserved memory` represents the total amount of memory our app can potentially use.  
Conversely, the `committed memory` is equal to the amount of memory our app is using right now.  

### 3. Heap
NMT reports our heap allocations as we expected:  

```
Java Heap (reserved=307200KB, committed=307200KB)
                            (mmap: reserved=307200KB, committed=307200KB)
```
300 MB of both reserved and committed memory, which matches our heap size settings.  

### 4. Metaspace
This is what NMT displays about the class metadata for loaded classes:  
```
Class (reserved=1091407KB, committed=45815KB)
      (classes #6566)
      (malloc=10063KB #8519) 
      (mmap: reserved=1081344KB, committed=35752KB)
```
Almost 1 GB reserved and 45 MB committed to loading 6566 classes.  

### 5. Thread
NMT report on thread allocations:  
```
Thread (reserved=33926KB, committed=33926KB)
                            (thread #34)
                            (stack: reserved=33792KB, committed=33792KB)
                            (malloc=95KB #178)
                            (arena=39KB #66)
```
In total, 32 MB of memory is allocated to stacks for 34 threads – almost 1 MB per stack.  
JVM allocates the memory to threads at the time of creation, so the reserved and committed allocations are equal.  

### 6. Code Cache
NMT displays about the generated and cached assembly instructions by JIT:  
```
Code (reserved=249638KB, committed=2574KB)
                            (malloc=38KB #313)
                            (mmap: reserved=249600KB, committed=2536KB)
```
Currently, almost 2.5 MB of code is being cached, and this amount can potentially go up to approximately 245 MB.

### 7. GC
NMT report about G1 GC's memory usage:  
```
GC (reserved=61731KB, committed=61731KB)
                            (malloc=17443KB #2019)
                            (mmap: reserved=44288KB, committed=44288KB)
```
As we can see, almost 60 MB is reserved and committed to helping `G1`.  

Let's see how the memory usage looks like for a much simpler GC, say Serial GC:  
```
java -XX:NativeMemoryTracking=summary -Xms300m -Xmx300m -XX:+UseSerialGC App.java
```
```
GC (reserved=1095KB, committed=1059KB)
                            (malloc=7KB #79)
                            (mmap: reserved=1088KB, committed=1052KB)
```

### 8. Symbol
NMT report about the symbol allocations, such as the `string table` and `constant pool`:  
```
Symbol (reserved=1366KB, committed=1366KB)
                            (malloc=911KB #99)
                            (arena=456KB #1)
```
Almost 1 MB is allocated to symbols.

### 9. NMT Over Time
The NMT allows us to track how memory allocations change over time  
First, we should mark the current state of our application as a baseline:  

```java
jcmd <pid> VM.native_memory baseline
```
Then, after a while, we can compare the current memory usage with that baseline:  
```java
jcmd <pid> VM.native_memory summary.diff
```
NMT, using + and – signs, would tell us how the memory usage changed over that period  
```
Total: reserved=1771487KB +3373KB, committed=491491KB +6873KB
		Class (reserved=1084300KB +2103KB, committed=39356KB +2871KB)
```
The total reserved and committed memory increased by 3 MB and 6 MB, respectively.  
Other fluctuations in memory allocations can be spotted as easily.  

### 10. Detailed NMT
NMT can provide very detailed information about a map of the entire memory space.  
To enable this detailed report, we should use the `-XX:NativeMemoryTracking`=**detail** tuning flag.  
```java
Virtual memory map:
 
[0x8f1c1000 - 0x8f467000] reserved 2712KB for Thread Stack
                from [Thread::record_stack_base_and_size()+0xca]
        [0x8f1c1000 - 0x8f467000] committed 2712KB from [Thread::record_stack_base_and_size()+0xca]
 
[0x8f585000 - 0x8f729000] reserved 1680KB for Thread Stack
                from [Thread::record_stack_base_and_size()+0xca]
        [0x8f585000 - 0x8f729000] committed 1680KB from [Thread::record_stack_base_and_size()+0xca]
 
[0x8f930000 - 0x90100000] reserved 8000KB for GC
                from [ReservedSpace::initialize(unsigned int, unsigned int, bool, char*, unsigned int, bool)+0x555]
        [0x8f930000 - 0x90100000] committed 8000KB from [PSVirtualSpace::expand_by(unsigned int)+0x95]
 
[0x902dd000 - 0x9127d000] reserved 16000KB for GC
                from [ReservedSpace::initialize(unsigned int, unsigned int, bool, char*, unsigned int, bool)+0x555]
        [0x902dd000 - 0x9127d000] committed 16000KB from [os::pd_commit_memory(char*, unsigned int, unsigned int, bool)+0x36]
 
[0x9127d000 - 0x91400000] reserved 1548KB for Thread Stack
                from [Thread::record_stack_base_and_size()+0xca]
        [0x9127d000 - 0x91400000] committed 1548KB from [Thread::record_stack_base_and_size()+0xca]
 
[0x91400000 - 0xb0c00000] reserved 516096KB for Java Heap                                                                            <--- reserved memory range
                from [ReservedSpace::initialize(unsigned int, unsigned int, bool, char*, unsigned int, bool)+0x190]                  <--- callsite that reserves the memory
        [0x91400000 - 0x93400000] committed 32768KB from [VirtualSpace::initialize(ReservedSpace, unsigned int)+0x3e8]               <--- committed memory range and its callsite
        [0xa6400000 - 0xb0c00000] committed 172032KB from [PSVirtualSpace::expand_by(unsigned int)+0x95]                             <--- committed memory range and its callsite
 
[0xb0c61000 - 0xb0ce2000] reserved 516KB for Thread Stack
                from [Thread::record_stack_base_and_size()+0xca]
        [0xb0c61000 - 0xb0ce2000] committed 516KB from [Thread::record_stack_base_and_size()+0xca]
 
[0xb0ce2000 - 0xb0e83000] reserved 1668KB for GC
                from [ReservedSpace::initialize(unsigned int, unsigned int, bool, char*, unsigned int, bool)+0x555]
        [0xb0ce2000 - 0xb0cf0000] committed 56KB from [PSVirtualSpace::expand_by(unsigned int)+0x95]
        [0xb0d88000 - 0xb0d96000] committed 56KB from [CardTableModRefBS::resize_covered_region(MemRegion)+0xebf]
        [0xb0e2e000 - 0xb0e83000] committed 340KB from [CardTableModRefBS::resize_covered_region(MemRegion)+0xebf]
 
[0xb0e83000 - 0xb7003000] reserved 99840KB for Code
                from [ReservedSpace::initialize(unsigned int, unsigned int, bool, char*, unsigned int, bool)+0x555]
        [0xb0e83000 - 0xb0e92000] committed 60KB from [VirtualSpace::initialize(ReservedSpace, unsigned int)+0x3e8]
        [0xb1003000 - 0xb139b000] committed 3680KB from [VirtualSpace::initialize(ReservedSpace, unsigned int)+0x37a]
 
[0xb7003000 - 0xb7603000] reserved 6144KB for Class
                from [ReservedSpace::initialize(unsigned int, unsigned int, bool, char*, unsigned int, bool)+0x555]
        [0xb7003000 - 0xb73a4000] committed 3716KB from [VirtualSpace::initialize(ReservedSpace, unsigned int)+0x37a]
 
[0xb7603000 - 0xb760b000] reserved 32KB for Internal
                from [PerfMemory::create_memory_region(unsigned int)+0x8ba]
 
[0xb770b000 - 0xb775c000] reserved 324KB for Thread Stack
                from [Thread::record_stack_base_and_size()+0xca]
        [0xb770b000 - 0xb775c000] committed 324KB from [Thread::record_stack_base_and_size()+0xca]
```

**Reference:**  
1. https://www.baeldung.com/native-memory-tracking-in-jvm

