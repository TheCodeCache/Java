# ArrayList vs LinkedList - 

In terms of theoretical time complexity vis-a-vis big-O notation, there is no difference.  
To iterate an ArrayList and to iterate a LinkedList are both O(n) operations.  
However, in practice, there is a very strong reason to prefer an ArrayList for modern processors.  

When iterating an ArrayList, the data will typically be loaded into cache first.  
The data is all physically adjacent in the memory layout,  
so pulling up the entire set of data using L2 cache (or perhaps even L1 cache for smaller arrays) is quite feasible.  
However, for a LinkedList, the memory for each element needs to be allocated and found separately.  
This implies that you will frequently need to access main memory instead of just accessing the cache.  


### Time complexity -  

![image](https://user-images.githubusercontent.com/26399543/191965414-1d3daac7-bafb-4f3e-ba3e-05ccd33cb4e7.png)  


