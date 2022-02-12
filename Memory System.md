# Java Memory System –

<h3> Memory </h3>  
The memory system of the Java virtual machine manages  
the following kinds of memory:  

<h3> 1. Heap </h3>  
The Java virtual machine has a <i>heap</i> that is the runtime  
data area from which memory for all class instances and arrays  
are allocated.  It is created at the Java virtual machine start-up.  
Heap memory for objects is reclaimed by an automatic memory management  
system which is known as a <i>garbage collector</i>.  

<p>The heap may be of a fixed size or may be expanded and shrunk.  
The memory for the heap does not need to be contiguous.  

<h3> 2. Non-Heap Memory</h3>  
The Java virtual machine manages memory other than the heap  
(referred as <i>non-heap memory</i>).  

<p> The Java virtual machine has a <i>method area</i> that is shared  
among all threads.  
The method area belongs to non-heap memory.  It stores per-class structures  
such as a runtime constant pool, field and method data, and the code for  
methods and constructors.  It is created at the Java virtual machine  
start-up.  

<p> The method area is logically part of the heap but a Java virtual  
machine implementation may choose not to either garbage collect  
or compact it.  Similar to the heap, the method area may be of a  
fixed size or may be expanded and shrunk.  The memory for the  
method area does not need to be contiguous.  

<p>In addition to the method area, a Java virtual machine  
implementation may require memory for internal processing or  
optimization which also belongs to non-heap memory.  
For example, the JIT compiler requires memory for storing the native  
machine code translated from the Java virtual machine code for  
high performance.  

<h3>Memory Pools and Memory Managers</h3>  
{@link MemoryPoolMXBean Memory pools} and  
{@link MemoryManagerMXBean memory managers} are the abstract entities  
that monitor and manage the memory system  
of the Java virtual machine.  

<p>A memory pool represents a memory area that the Java virtual machine  
manages.  The Java virtual machine has at least one memory pool  
and it may create or remove memory pools during execution.  
A memory pool can belong to either the heap or the non-heap memory.  

<p>A memory manager is responsible for managing one or more memory pools.  
The garbage collector is one type of memory manager responsible  
for reclaiming memory occupied by unreachable objects.  A Java virtual  
machine may have one or more memory managers.   It may  
add or remove memory managers during execution.  
A memory pool can be managed by more than one memory manager.  

**Reference:**    
1. java.lang.management.MemoryMXBean

