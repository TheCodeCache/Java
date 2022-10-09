# Green Threads - 

Typically this works by running several native threads and then allocating the green threads onto these native threads for execution  

Native threads are very efficient to run, but they have a high cost around starting and stopping them.  
Green threads help to avoid this cost and give the architecture a lot more flexibility.  
If we are using relatively long-running threads, then native threads are very efficient.  
For very short-lived jobs, the cost of starting them can outweigh the benefit of using them.  
In these cases, green threads can become more efficient.  
  
Java does not have built-in support for green threads.  

# Native Threads - 
The standard way of implementing multi-tasking in Java is to use threads.  
Threading is usually supported down to the operating system. We call threads that work at this level “native threads”.  

The operating system has some abilities with threading that are often unavailable to our applications,  
simply because of how much closer it is to the underlying hardware.  
This means that executing native threads are typically more efficient.  
These threads directly map to threads of execution on the computer CPU –  
and the operating system manages the mapping of threads onto CPU cores.  

The standard threading model in Java, covering all JVM languages, uses native threads  

