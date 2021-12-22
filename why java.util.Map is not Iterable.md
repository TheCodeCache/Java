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

# `Map` In `Scala` collections:

However, in Scala collections hierarchy,  
`Map` extends `Iterable` and it does provide the default iteration based on the key-value entries/pairs.  
For ex:  

```scala
val names = Map("fname" -> "Manoranjan", "lname" -> "Kumar")

for (pair <- names){
  println(s"key: $pair._1")
  println(s"value: $pair._2")
}

for (key <- names.keys){
  println(s"key: $key")
}

for (value <- names.values){
  println(s"value: value")
}

for (entry <- names.entry){ // names.entry does not exist, it's a compile time error
  // inspect entry object (if found)
}
```

so, the point here is:  
many a times, it depends on the library designer whether to expose a functionality in a certain way or not!  

**References**:  
1. https://stackoverflow.com/a/11507849/6842300
2. https://stackoverflow.com/a/19422495/6842300

