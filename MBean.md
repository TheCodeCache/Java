# MBean (Managed Bean) –

A `MBean` ia a **managed java object**, similar to a **JavaBeans** component,  
that follows the design patterns mentioned in JMX specification.  

An MBean can represent a device (printer etc.), an application, system objects,  
service-oriented networks, or any resource, that needs to be managed  

The JVM specification defines 5 types of MBean:  

- **Standard** MBean
- **Dynamic** MBean
- **Open** MBean
- **Model** MBean
- **MXBean**

### For Example: 

**Demonstration of a `Standard Bean` –**  

```java
package com.thecodecache.mbeans;

/**
 * MBean
 * 
 * @author manoranjan.kumar
 */
public interface GameMBean {

	public void playFootball(String clubName);

	public String getPlayerName();

	public void setPlayerName(String playerName);
}
```

```java
package com.thecodecache.mbeans;

public class Game implements GameMBean {

	private String playerName;

	@Override
	public void playFootball(String clubName) {
		System.out.println(this.playerName + " playing football for " + clubName);
	}

	@Override
	public String getPlayerName() {
		System.out.println("Return playerName " + this.playerName);
		return playerName;
	}

	@Override
	public void setPlayerName(String playerName) {
		System.out.println("Set playerName to value " + playerName);
		this.playerName = playerName;
	}
}
```

```java
package com.thecodecache.mbeans;

import java.io.IOException;
import java.lang.management.ManagementFactory;

import javax.management.InstanceAlreadyExistsException;
import javax.management.MBeanRegistrationException;
import javax.management.MBeanServer;
import javax.management.MalformedObjectNameException;
import javax.management.NotCompliantMBeanException;
import javax.management.ObjectName;

/**
 * JMX Agent
 * 
 * @author manoranjan.kumar
 */
public class Main {

	public static void main(String[] args) {
		System.out.println("main entry point");
		try {
			ObjectName objectName = new ObjectName("com.thecodecache.mbeans:type=basic,name=game");
			MBeanServer server = ManagementFactory.getPlatformMBeanServer();
			server.registerMBean(new Game(), objectName);
		} catch (MalformedObjectNameException | InstanceAlreadyExistsException | MBeanRegistrationException
				| NotCompliantMBeanException e1) {
			System.out.println("Exception Caught !!");
			e1.printStackTrace();
		}

		int code;
		try {
			code = System.in.read(); // to stop the JVM from exit so that we could troubleshoot
			System.out.println("user entered exit code: " + code);
		} catch (IOException e) {
			e.printStackTrace();
		}
		System.out.println("Exit!");
	}
}
```



**Open up the `JConsole` from the JDK /bin installation directory** –  

![image](https://user-images.githubusercontent.com/26399543/153718330-8af4d7e0-7e4a-47e1-8cea-8dff49792679.png)  

![image](https://user-images.githubusercontent.com/26399543/153718354-0ee0ec54-1851-4c0f-b978-a317c2e49998.png)  

![image](https://user-images.githubusercontent.com/26399543/153718415-d2edef93-4c0b-4af3-b4e0-86dac121fd3a.png)  

![image](https://user-images.githubusercontent.com/26399543/153718431-2e87bb0f-96a9-4e8a-886f-06d9a1e09a7c.png)  

![image](https://user-images.githubusercontent.com/26399543/153718457-e4cd73ae-c2bb-4b31-897f-b3f499f71fe2.png)  

![image](https://user-images.githubusercontent.com/26399543/153718481-eff24f09-8101-4fd9-ac83-a7a2237fa934.png)  

![image](https://user-images.githubusercontent.com/26399543/153718493-631c5313-563e-45b9-9851-281095c82440.png)  

![image](https://user-images.githubusercontent.com/26399543/153718551-dbc76b6c-330c-4c61-ae77-d3c1d248712a.png)  

**Eclipse Standard Console –**  

![image](https://user-images.githubusercontent.com/26399543/153718560-aa839031-3704-4475-8902-188dc7ffabee.png)  

![image](https://user-images.githubusercontent.com/26399543/153718570-9d1dfe8f-8404-41d8-866b-a1ba52a62c14.png)  

![image](https://user-images.githubusercontent.com/26399543/153718601-3d169901-7ad5-4aa4-aa88-ca0935c53072.png)  

![image](https://user-images.githubusercontent.com/26399543/153718630-e952194e-114c-4712-946e-467f17f56245.png)  

**Eclipse Standard Console –**  

![image](https://user-images.githubusercontent.com/26399543/153718656-08697bf8-0d6b-491d-a85a-d36ba41a95c3.png)  


**Reference:**  
1. https://www.baeldung.com/java-management-extensions

