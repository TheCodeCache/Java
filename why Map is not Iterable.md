# why `java.util.Map<T>` is not `Iterable`

`Map` in general (and HashMap in particular) do not implement `Iterator`  
> because it is not clear what it should be iterating.  

So, there are three choices:  
1. Keys
2. Values
3. Entries

We can't iterate over a `Map` directly because there are three types of iteration that a Map supports  
and there was no clear reason to choose one or the other.  
Doing the equivalent entrySet().iterator() may have been reasonable, but it's not the choice which was made by the library designer.  

The library designers decided not to make this choice, letting programmers pick what to iterate explicitly.  

**References**:  
1. https://stackoverflow.com/a/11507849/6842300
2. https://stackoverflow.com/a/19422495/6842300

