# Direct Byte Buffers — 

A byte buffer is either direct or non-direct.  
Given a `direct byte buffer`, the Java virtual machine will make a best effort to perform native I/O operations directly upon it.  
That is, it will attempt  
to avoid copying the buffer's content to (or from) an intermediate buffer before (or after) each invocation of  
one of the underlying operating system's native I/O operations.  

