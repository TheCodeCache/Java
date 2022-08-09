# Memory Concepts in Java:

Memory Management is all about `Garbage Collection` i.e. `GC` in java  

`GC` runs on Heap memory.  

`Heap Memory` is bifurcated into following memory segments:  
1. Young Generation
   - Eden Space
   - Survivor Space 1
   - Survivor Space 2
2. Old Generation

![image](https://user-images.githubusercontent.com/26399543/183639504-7b03b326-2f69-4593-b264-6f246e5d3c70.png)  

**PremGen**: MetaData information of classes was stored in PremGen (Permanent-Generation) memory type before Java 8.  
**PremGen** is fixed in size and cannot be dynamically resized. It was a contiguous Java Heap Memory.  

**MetaSpace**: Java 8 stores the MetaData of classes in native memory called 'MetaSpace'.  
It is not a contiguous Heap Memory and hence can be grown dynamically which helps to overcome the size constraints.  
This improves the garbage collection, auto-tuning, and de-allocation of metadata  

![image](https://user-images.githubusercontent.com/26399543/183647457-af2fcc14-cc71-4e38-a726-f0086c3d4613.png)  


Reference:  
- https://stackoverflow.com/a/40899996/6842300  

