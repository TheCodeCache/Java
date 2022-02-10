# Code Quality – 

[SonarQube](https://www.sonarqube.org/) is used for Code Quality analysis.  
It supports multiple languages like Java/Python etc.  

## Steps to be followed:  

### 1. Set up sonar server in local 
Need to download this binary in order to set up the sonar server in local.  

https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.3.0.51899.zip  
Please check for the latest version though.  

```shell
C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\bin\windows-x86-64>StartSonar.bat
wrapper  | --> Wrapper Started as Console
wrapper  | Launching a JVM...
jvm 1    | Wrapper (Version 3.2.3) http://wrapper.tanukisoftware.org
jvm 1    |   Copyright 1999-2006 Tanuki Software, Inc.  All Rights Reserved.
jvm 1    |
jvm 1    | 2022.02.11 03:04:05 INFO  app[][o.s.a.AppFileSystem] Cleaning or creating temp directory C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp
jvm 1    | 2022.02.11 03:04:05 INFO  app[][o.s.a.es.EsSettings] Elasticsearch listening on [HTTP: 127.0.0.1:9001, TCP: 127.0.0.1:54300]
jvm 1    | 2022.02.11 03:04:06 INFO  app[][o.s.a.ProcessLauncherImpl] Launch process[[key='es', ipcIndex=1, logFilenamePrefix=es]] from [C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\elasticsearch]: C:\Program Files\Java\jdk-11.0.14\bin\java -XX:+UseG1GC -Djava.io.tmpdir=C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp -XX:ErrorFile=../logs/es_hs_err_pid%p.log -Des.networkaddress.cache.ttl=60 -Des.networkaddress.cache.negative.ttl=10 -XX:+AlwaysPreTouch -Xss1m -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djna.nosys=true -Djna.tmpdir=C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp -XX:-OmitStackTraceInFastThrow -Dio.netty.noUnsafe=true -Dio.netty.noKeySetOptimization=true -Dio.netty.recycler.maxCapacityPerThread=0 -Dio.netty.allocator.numDirectArenas=0 -Dlog4j.shutdownHookEnabled=false -Dlog4j2.disable.jmx=true -Dlog4j2.formatMsgNoLookups=true -Djava.locale.providers=COMPAT -Dcom.redhat.fips=false -Xmx512m -Xms512m -XX:MaxDirectMemorySize=256m -XX:+HeapDumpOnOutOfMemoryError -Delasticsearch -Des.path.home=C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\elasticsearch -Des.path.conf=C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp\conf\es -cp lib/* org.elasticsearch.bootstrap.Elasticsearch
jvm 1    | 2022.02.11 03:04:07 INFO  app[][o.s.a.SchedulerImpl] Waiting for Elasticsearch to be up and running
jvm 1    | 2022.02.11 03:04:52 INFO  app[][o.s.a.SchedulerImpl] Process[es] is up
jvm 1    | 2022.02.11 03:04:52 INFO  app[][o.s.a.ProcessLauncherImpl] Launch process[[key='web', ipcIndex=2, logFilenamePrefix=web]] from [C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899]: C:\Program Files\Java\jdk-11.0.14\bin\java -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djava.io.tmpdir=C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp -XX:-OmitStackTraceInFastThrow --add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-opens=java.rmi/sun.rmi.transport=ALL-UNNAMED --add-exports=java.base/jdk.internal.ref=ALL-UNNAMED --add-opens=java.base/java.nio=ALL-UNNAMED --add-opens=java.base/sun.nio.ch=ALL-UNNAMED --add-opens=java.management/sun.management=ALL-UNNAMED --add-opens=jdk.management/com.sun.management.internal=ALL-UNNAMED -Dcom.redhat.fips=false -Xmx512m -Xms128m -XX:+HeapDumpOnOutOfMemoryError -Dhttp.nonProxyHosts=localhost|127.*|[::1] -cp ./lib/sonar-application-9.3.0.51899.jar;C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\lib\jdbc\h2\h2-1.4.199.jar org.sonar.server.app.WebServer C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp\sq-process8862223959619986879properties
jvm 1    | 2022.02.11 03:08:29 INFO  app[][o.s.a.SchedulerImpl] Process[web] is up
jvm 1    | 2022.02.11 03:08:29 INFO  app[][o.s.a.ProcessLauncherImpl] Launch process[[key='ce', ipcIndex=3, logFilenamePrefix=ce]] from [C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899]: C:\Program Files\Java\jdk-11.0.14\bin\java -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djava.io.tmpdir=C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp -XX:-OmitStackTraceInFastThrow --add-opens=java.base/java.util=ALL-UNNAMED --add-exports=java.base/jdk.internal.ref=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.nio=ALL-UNNAMED --add-opens=java.base/sun.nio.ch=ALL-UNNAMED --add-opens=java.management/sun.management=ALL-UNNAMED --add-opens=jdk.management/com.sun.management.internal=ALL-UNNAMED -Dcom.redhat.fips=false -Xmx512m -Xms128m -XX:+HeapDumpOnOutOfMemoryError -Dhttp.nonProxyHosts=localhost|127.*|[::1] -cp ./lib/sonar-application-9.3.0.51899.jar;C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\lib\jdbc\h2\h2-1.4.199.jar org.sonar.ce.app.CeServer C:\Users\U1159927\Desktop\marsh\tools_soft\sonarqube-9.3.0.51899\temp\sq-process16843441843490891922properties
jvm 1    | 2022.02.11 03:08:37 WARN  app[][startup] ####################################################################################################################
jvm 1    | 2022.02.11 03:08:37 WARN  app[][startup] Default Administrator credentials are still being used. Make sure to change the password or deactivate the account.
jvm 1    | 2022.02.11 03:08:37 WARN  app[][startup] ####################################################################################################################
jvm 1    | 2022.02.11 03:08:48 INFO  app[][o.s.a.SchedulerImpl] Process[ce] is up
jvm 1    | 2022.02.11 03:08:48 INFO  app[][o.s.a.SchedulerImpl] SonarQube is up
```

The sonar web server is up at `http://localhost:9000/`  
Go to browser and hit [http://localhost:9000/](http://localhost:9000/) url

Just login using admin/admin credential and change todummy credential,

Disable `Force user authentication` by navigating as follows:  
Navigate to Administration -> Configuration -> Security -> Force user authentication  

### 2. Install Java - Oracle JDK 11 
SonarQube supports Java 11 or newer  

```shell
C:\Users\U1159927>java -version
java version "11.0.14" 2022-01-18 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.14+8-LTS-263)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.14+8-LTS-263, mixed mode)
```

### 3. Code Changes 

**pom.xml**  

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.thecodecache</groupId>
	<artifactId>sonar-code-quality</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>sonar-code-quality</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
	<build>
		<sourceDirectory>${project.basedir}/src/main/java</sourceDirectory>
		<testSourceDirectory>${project.basedir}/src/test/java</testSourceDirectory>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.9.0</version>
				<configuration>
					<release>11</release>
				</configuration>
			</plugin>
			<!-- https://mvnrepository.com/artifact/org.sonarsource.scanner.maven/sonar-maven-plugin -->
			<plugin>
				<groupId>org.sonarsource.scanner.maven</groupId>
				<artifactId>sonar-maven-plugin</artifactId>
				<version>3.9.1.2184</version>
			</plugin>

			<!-- https://mvnrepository.com/artifact/org.jacoco/jacoco-maven-plugin -->
			<plugin>
				<groupId>org.jacoco</groupId>
				<artifactId>jacoco-maven-plugin</artifactId>
				<version>0.8.7</version>

				<executions>
					<execution>
						<!-- this prepare-agent reads the details of line under execution from JVM -->
						<id>prepare-agent</id>
						<goals>
							<goal>prepare-agent</goal>
						</goals>
					</execution>
					<execution>
						<id>report</id>
						<phase>prepare-package</phase>
						<goals>
							<goal>report</goal>
						</goals>
					</execution>
					<execution>
						<id>post-unit-test</id>
						<phase>test</phase>
						<goals>
							<goal>report</goal>
						</goals>
						<configuration>
							<!-- Sets the path to the file which contains the execution data. -->
							<dataFile>target/jacoco.exec</dataFile>
							<!-- Sets the output directory for the code coverage report. -->
							<outputDirectory>target/my-reports</outputDirectory>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
</project>
```

**App.java**  

```java
package com.thecodecache.sonar_code_quality;

import java.util.ArrayList;
import java.util.List;

/**
 * Class under Quality Control Test
 */
public class App {

	public void m1() {
		// String s = "";
		List<Integer> list = new ArrayList<Integer>();
		list.add(1);
		list.add(2);

		Object obj = getData();
		if (obj != null) {
			System.out.println(obj.toString());
		}
	}

	public Object getData() {
		return null;
	}

	public static void main(String[] args) {
		App app = new App();
		app.m1();
	}
}
```

**AppTest.java**  

```java
package com.thecodecache.sonar_code_quality;

import junit.framework.Test;
import junit.framework.TestCase;
import junit.framework.TestSuite;

/**
 * Unit test for simple App.
 */
public class AppTest extends TestCase {
	/**
	 * Create the test case
	 *
	 * @param testName name of the test case
	 */
	public AppTest(String testName) {
		super(testName);
	}

	/**
	 * @return the suite of tests being tested
	 */
	public static Test suite() {
		return new TestSuite(AppTest.class);
	}

	/**
	 * Rigourous Test :-)
	 */
	public void testApp() {

		App a = new App();
		a.m1();
		a.getData();
		assertTrue(true);
	}
}
```

**Project directory Structure:**  

![image](https://user-images.githubusercontent.com/26399543/153510489-6e7d89fc-1778-4c9b-8e79-eefc02e2c8c6.png)  

### 4. Build the Application

Run this cmd either through cmd line or through Eclipse/IDE  
`maven clean install`  
no need to run prepare-agent as it is already part of the goal in JaCOCO plugin defined in pom.xml  
so, `mvn install` phase will trigger the JaCoCo plugin which generates the coverage report  

and then,  
Run this cmd as well for `sonar` reports  
`mvn sonar:sonar`  
sample build output:  
```
[INFO] Scanning for projects...
[INFO] 
[INFO] ----------------< com.thecodecache:sonar-code-quality >-----------------
[INFO] Building sonar-code-quality 0.0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- sonar-maven-plugin:3.9.1.2184:sonar (default-cli) @ sonar-code-quality ---
[INFO] User cache: C:\Users\U1159927\.sonar\cache
[INFO] SonarQube version: 9.3.0
[INFO] Default locale: "en_US", source code encoding: "UTF-8"
[INFO] Load global settings
[INFO] Load global settings (done) | time=362ms
[INFO] Server id: BF41A1F2-AX7lj_Qo3NC0lAWjhAhq
[INFO] User cache: C:\Users\U1159927\.sonar\cache
[INFO] Load/download plugins
[INFO] Load plugins index
[INFO] Load plugins index (done) | time=288ms
[INFO] Load/download plugins (done) | time=607ms
[INFO] Process project properties
[INFO] Process project properties (done) | time=18ms
[INFO] Execute project builders
[INFO] Execute project builders (done) | time=3ms
[INFO] Project key: com.thecodecache:sonar-code-quality
[INFO] Base dir: C:\Users\U1159927\Desktop\marsh\code\tests\sonar-code-quality
[INFO] Working dir: C:\Users\U1159927\Desktop\marsh\code\tests\sonar-code-quality\target\sonar
[INFO] Load project settings for component key: 'com.thecodecache:sonar-code-quality'
[INFO] Load project settings for component key: 'com.thecodecache:sonar-code-quality' (done) | time=22ms
[INFO] Load quality profiles
[INFO] Load quality profiles (done) | time=130ms
[INFO] Load active rules
[INFO] Load active rules (done) | time=3375ms
[INFO] Indexing files...
[INFO] Project configuration:
[INFO] 3 files indexed
[INFO] 0 files ignored because of scm ignore settings
[INFO] Quality profile for java: Sonar way
[INFO] Quality profile for xml: Sonar way
[INFO] ------------- Run sensors on module sonar-code-quality
[INFO] Load metrics repository
[INFO] Load metrics repository (done) | time=44ms
[ERROR] Creating lock file P:\.config\jgit\config.lock failed
java.io.IOException: Access is denied
	at java.base/java.io.WinNTFileSystem.createFileExclusively(Native Method)
	at java.base/java.io.File.createNewFile(File.java:1035)
	at org.eclipse.jgit.util.FS.createNewFileAtomic(FS.java:1778)
	at org.eclipse.jgit.internal.storage.file.LockFile.lock(LockFile.java:140)
	at org.eclipse.jgit.storage.file.FileBasedConfig.save(FileBasedConfig.java:219)
	at org.eclipse.jgit.util.FS$FileStoreAttributes.saveToConfig(FS.java:740)
	at org.eclipse.jgit.util.FS$FileStoreAttributes.lambda$4(FS.java:426)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:834)

[ERROR] Cannot save config file 'FileBasedConfig[P:\.config\jgit\config]'
java.io.IOException: Access is denied
	at java.base/java.io.WinNTFileSystem.createFileExclusively(Native Method)
	at java.base/java.io.File.createNewFile(File.java:1035)
	at org.eclipse.jgit.util.FS.createNewFileAtomic(FS.java:1778)
	at org.eclipse.jgit.internal.storage.file.LockFile.lock(LockFile.java:140)
	at org.eclipse.jgit.storage.file.FileBasedConfig.save(FileBasedConfig.java:219)
	at org.eclipse.jgit.util.FS$FileStoreAttributes.saveToConfig(FS.java:740)
	at org.eclipse.jgit.util.FS$FileStoreAttributes.lambda$4(FS.java:426)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1128)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
	at java.base/java.lang.Thread.run(Thread.java:834)

[INFO] Sensor JavaSensor [java]
[INFO] Configured Java source version (sonar.java.source): 11
[INFO] JavaClasspath initialization
[INFO] JavaClasspath initialization (done) | time=11ms
[INFO] JavaTestClasspath initialization
[INFO] JavaTestClasspath initialization (done) | time=10ms
[INFO] Java "Main" source files AST scan
[INFO] 1 source file to be analyzed
[INFO] Load project repositories
[INFO] Load project repositories (done) | time=29ms
[INFO] 1/1 source file has been analyzed
[INFO] Java "Main" source files AST scan (done) | time=3318ms
[INFO] Java "Test" source files AST scan
[INFO] 1 source file to be analyzed
[INFO] 1/1 source file has been analyzed
[INFO] Java "Test" source files AST scan (done) | time=281ms
[INFO] No "Generated" source files to scan.
[INFO] Sensor JavaSensor [java] (done) | time=4307ms
[INFO] Sensor JaCoCo XML Report Importer [jacoco]
[INFO] 'sonar.coverage.jacoco.xmlReportPaths' is not defined. Using default locations: target/site/jacoco/jacoco.xml,target/site/jacoco-it/jacoco.xml,build/reports/jacoco/test/jacocoTestReport.xml
[INFO] Importing 1 report(s). Turn your logs in debug mode in order to see the exhaustive list.
[INFO] Sensor JaCoCo XML Report Importer [jacoco] (done) | time=60ms
[INFO] Sensor CSS Rules [javascript]
[INFO] No CSS, PHP, HTML or VueJS files are found in the project. CSS analysis is skipped.
[INFO] Sensor CSS Rules [javascript] (done) | time=1ms
[INFO] Sensor C# Project Type Information [csharp]
[INFO] Sensor C# Project Type Information [csharp] (done) | time=1ms
[INFO] Sensor C# Analysis Log [csharp]
[INFO] Sensor C# Analysis Log [csharp] (done) | time=60ms
[INFO] Sensor C# Properties [csharp]
[INFO] Sensor C# Properties [csharp] (done) | time=0ms
[INFO] Sensor SurefireSensor [java]
[INFO] parsing [C:\Users\U1159927\Desktop\marsh\code\tests\sonar-code-quality\target\surefire-reports]
[INFO] Sensor SurefireSensor [java] (done) | time=321ms
[INFO] Sensor HTML [web]
[INFO] Sensor HTML [web] (done) | time=8ms
[INFO] Sensor XML Sensor [xml]
[INFO] 1 source file to be analyzed
[INFO] 1/1 source file has been analyzed
[INFO] Sensor XML Sensor [xml] (done) | time=484ms
[INFO] Sensor Text Sensor [text]
[INFO] 3 source files to be analyzed
[INFO] 3/3 source files have been analyzed
[INFO] Sensor Text Sensor [text] (done) | time=49ms
[INFO] Sensor VB.NET Project Type Information [vbnet]
[INFO] Sensor VB.NET Project Type Information [vbnet] (done) | time=3ms
[INFO] Sensor VB.NET Analysis Log [vbnet]
[INFO] Sensor VB.NET Analysis Log [vbnet] (done) | time=19ms
[INFO] Sensor VB.NET Properties [vbnet]
[INFO] Sensor VB.NET Properties [vbnet] (done) | time=1ms
[INFO] ------------- Run sensors on project
[INFO] Sensor Zero Coverage Sensor
[INFO] Sensor Zero Coverage Sensor (done) | time=1ms
[INFO] Sensor Java CPD Block Indexer
[INFO] Sensor Java CPD Block Indexer (done) | time=28ms
[INFO] SCM Publisher SCM provider for this project is: git
[INFO] SCM Publisher 3 source files to be analyzed
[INFO] SCM Publisher 0/3 source files have been analyzed (done) | time=547ms
[WARNING] Missing blame information for the following files:
[WARNING]   * src/main/java/com/thecodecache/sonar_code_quality/App.java
[WARNING]   * src/test/java/com/thecodecache/sonar_code_quality/AppTest.java
[WARNING]   * pom.xml
[WARNING] This may lead to missing/broken features in SonarQube
[INFO] CPD Executor Calculating CPD for 1 file
[INFO] CPD Executor CPD calculation finished (done) | time=10ms
[INFO] Analysis report generated in 358ms, dir size=119.8 kB
[INFO] Analysis report compressed in 126ms, zip size=19.1 kB
[INFO] Analysis report uploaded in 33ms
[INFO] ANALYSIS SUCCESSFUL, you can browse http://localhost:9000/dashboard?id=com.thecodecache%3Asonar-code-quality
[INFO] Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
[INFO] More about the report processing at http://localhost:9000/api/ce/task?id=AX7lwk9w3NC0lAWjhF4O
[INFO] Analysis total time: 21.787 s
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  27.806 s
[INFO] Finished at: 2022-02-11T04:00:24+05:30
[INFO] ------------------------------------------------------------------------
```

### 5. Open SonarQube Dashboard

Validate the quality reports  

PFB the sample screen shot  

**home page:**  
<img src="https://user-images.githubusercontent.com/26399543/153511284-eb6031eb-a2ae-4db5-8542-f2741452596f.png" width="80%" height="80%">  

**Issues:**  
<img src="https://user-images.githubusercontent.com/26399543/153511515-4aa1e78f-88f3-4a36-9ece-812ba1730ab3.png" width="80%" height="80%">  


Now, just create a plain simple maven project in Eclipse or any IDE of your choice.  


