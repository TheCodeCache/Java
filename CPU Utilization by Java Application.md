# CPU Usage by Java Application – 

### 1. Use `Java Mission Control`
```java
package com.thecodecache.mbeans;

import java.lang.management.ManagementFactory;
import java.lang.management.MemoryMXBean;
import java.lang.management.MemoryUsage;
import java.util.ArrayList;
import java.util.List;

import javax.swing.JOptionPane;

public class UsageOfCPUandMemoryBeanExample {

	private static List<String> list = new ArrayList<>();

	public static void main(String[] args) {
		JOptionPane.showMessageDialog(null, "Ready to Go?");
		while (true) {
			for (long i = 0; i < 100000; i++) {
				list.add("" + i);
			}
			if (calculatePercentageMemoryUsed() > 85) {
				System.out.println("Over 85% Utilization!");
				list.clear();
				JOptionPane.showMessageDialog(null, "List cleared!");
			}
		}
	}

	private static int calculatePercentageMemoryUsed() {
		MemoryMXBean memorybean = ManagementFactory.getMemoryMXBean();

		MemoryUsage heapUsage = memorybean.getHeapMemoryUsage();
		long usedMemory = heapUsage.getUsed();
		long maxMemory = heapUsage.getMax();

		int percentageUsed = (int) (100.0 * ((1.0 * usedMemory) / (1.0 * maxMemory)));

		System.out.println("Used vs Max Memory: " + usedMemory + "M/" + maxMemory + "M , " + percentageUsed
				+ "% List size: " + list.size());

		return percentageUsed;
	}
}
```

![image](https://user-images.githubusercontent.com/26399543/153720527-d16d9425-70cd-4aa1-b945-fb967109147b.png)  

### 2. `HPROF`: A CPU/Heap Profiling Tool 

![image](https://user-images.githubusercontent.com/26399543/153721226-bdef3c54-2ebb-4727-ac62-1dffd9ce4335.png)  



![image](https://user-images.githubusercontent.com/26399543/153721418-b5321d83-5a20-40c2-9c30-3dd3f18a1924.png)  

```java
CPU SAMPLES BEGIN (total = 71) Sat Feb 12 22:53:20 2022
rank   self  accum   count trace method
   1 21.13% 21.13%      15 300253 java.io.RandomAccessFile.readBytes
   2  8.45% 29.58%       6 300131 java.lang.ClassLoader.defineClass1
   3  4.23% 33.80%       3 300247 java.io.RandomAccessFile.open0
   4  4.23% 38.03%       3 300252 java.io.WinNTFileSystem.canonicalize0
   5  2.82% 40.85%       2 300245 java.io.WinNTFileSystem.getLastModifiedTime
   6  2.82% 43.66%       2 300168 java.util.zip.ZipFile.read
   7  2.82% 46.48%       2 300178 java.lang.ClassLoader.loadClass
   8  2.82% 49.30%       2 300173 java.util.zip.ZipFile.getEntry
   9  1.41% 50.70%       1 300254 java.lang.ClassLoader.loadClass
  10  1.41% 52.11%       1 300255 com.sun.tools.javac.code.Scope$3$1.<init>
  11  1.41% 53.52%       1 300251 java.util.ArrayList$Itr.next
  12  1.41% 54.93%       1 300250 java.io.WinNTFileSystem.getBooleanAttributes
  13  1.41% 56.34%       1 300249 java.lang.System.currentTimeMillis
  14  1.41% 57.75%       1 300248 java.lang.Object.getClass
  15  1.41% 59.15%       1 300265 java.io.RandomAccessFile.readBytes
  16  1.41% 60.56%       1 300246 java.lang.StringCoding$StringDecoder.decode
  17  1.41% 61.97%       1 300269 java.lang.Object.hashCode
  18  1.41% 63.38%       1 300270 com.sun.tools.javac.code.Symbol$MethodSymbol.implementation
  19  1.41% 64.79%       1 300239 java.lang.System.currentTimeMillis
  20  1.41% 66.20%       1 300234 java.io.File.listFiles
  21  1.41% 67.61%       1 300232 com.sun.tools.javac.parser.JavacParser.newEndPosTable
  22  1.41% 69.01%       1 300223 sun.misc.URLClassPath$3.run
  23  1.41% 70.42%       1 300214 java.util.regex.Pattern$CharProperty.complement
  24  1.41% 71.83%       1 300182 com.sun.tools.javac.jvm.Gen.<init>
  25  1.41% 73.24%       1 300181 java.util.zip.ZipFile.getEntryTime
  26  1.41% 74.65%       1 300179 com.sun.tools.javac.comp.Infer.<init>
  27  1.41% 76.06%       1 300271 java.lang.Object.getClass
  28  1.41% 77.46%       1 300177 com.sun.tools.javac.comp.Resolve.<init>
  29  1.41% 78.87%       1 300176 java.security.AccessController.doPrivileged
  30  1.41% 80.28%       1 300175 java.util.zip.ZipFile.getEntryBytes
  31  1.41% 81.69%       1 300174 java.util.zip.ZipFile.getEntryCSize
  32  1.41% 83.10%       1 300277 java.util.zip.ZipFile.getEntry
  33  1.41% 84.51%       1 300172 java.lang.System.nanoTime
  34  1.41% 85.92%       1 300240 java.util.zip.ZipFile.open
  35  1.41% 87.32%       1 300167 java.util.zip.ZipCoder.getBytes
  36  1.41% 88.73%       1 300162 java.lang.Class.getDeclaredConstructors0
  37  1.41% 90.14%       1 300036 java.io.FileOutputStream.close0
  38  1.41% 91.55%       1 300147 java.io.WinNTFileSystem.canonicalize0
  39  1.41% 92.96%       1 300278 java.util.HashMap.getNode
  40  1.41% 94.37%       1 300136 sun.misc.Unsafe.compareAndSwapObject
  41  1.41% 95.77%       1 300133 java.lang.ClassLoader.findBootstrapClass
  42  1.41% 97.18%       1 300139 java.util.ResourceBundle.<clinit>
  43  1.41% 98.59%       1 300118 sun.security.util.DisabledAlgorithmConstraints$KeySizeConstraint.<init>
  44  1.41% 100.00%       1 300056 java.util.zip.ZipFile.<init>
CPU SAMPLES END
```

**CPU Profiled output files–**  

[java.hprof.txt](https://github.com/TheCodeCache/Java/files/8054160/java.hprof.txt)  

[agentlib-hprof.txt](https://github.com/TheCodeCache/Java/files/8054159/agentlib-hprof.txt)  

[Xrunhprof.txt](https://github.com/TheCodeCache/Java/files/8054161/Xrunhprof.txt)  


**Reference:**  
1. https://docs.oracle.com/javase/7/docs/technotes/samples/hprof.html
2. JMC - Java Mission Control

