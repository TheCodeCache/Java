
Let us assume that the finalize method in Object class is public,  
The following class uses an IO connection and closes the connection in the finalize method.  

```java
class IOTest
{
    FileInputStream fis;
    // some code
    void writeInfo()
    {
        // write info to file using fis
    }
    // some code
    // some code
    public void finalize()   // can't be declared protected as it is public in Object class
    {
         try{fis.close();}
         catch(Exception e){}
    }
}

############# somewhere in a different packages

class UseIOTest
{
    public static void main(String[] args)
    {
        IOTest iTest = new IOTest();
        iTest.finalize();             // closes the connection
        iTest.writeInfo();            // will always throw IOException as the connection has been closed
    }
}
```

So, the object stored in reference iTest becomes wasted when you call the finalize method,  
that's why the finalize method in Object class is protected,  
Our class can then volunteer to make the finalize method public but that's not needed in practice.  

**Reference:**  
1. https://coderanch.com/t/269988/certification/clone-method-finalize-method-object



