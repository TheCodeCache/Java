The easiest way to create a `singleton` object is using `Enum`.  

```java
public enum Singleton {

	INSTANCE;

	private int count;

	// we should guard this function, when exposed to multiple threads to avoid race condition.  
	public void setCount(int count) {
		this.count = count;
	}

	public void doProcess() {
		System.out.println("Do high memory or CPU consume operation. count :-" + this.count);
	}
}
```

How to call the singleton instance?  

```java
Singleton.INSTANCE.doProcess();
```

This is the simple test case for verifying single instance use for each initialization.  

```java
@Test
public void singletonTest() {
  Singleton.INSTANCE.setCount(1);
  Singleton.INSTANCE.setCount(2);
  Singleton.INSTANCE.doProcess();
  Singleton.INSTANCE.doProcess();
  Singleton.INSTANCE.doProcess();
}
```

Pros:  
- An Instance is thread-safe.
- Easy to implement.  

Cons:  
- Eager initialization



**Reference:**  
1. https://www.codingame.com/playgrounds/6273/design-pattern-singleton-using-enum

