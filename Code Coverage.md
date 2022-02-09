# Code Coverage – 

**JaCoCo** stands for `Ja`va `Co`de `Co`verage

We could use `JaCoCo` tool to get the code coverage details.  
It generates a colorful report showing the code-path covered by running all the Unit Tests.  
This code coverage would give us the good insight on how much code is on the path of runtime execution.  
WE could get rid of the not reachable code.  
However, before removing un-reachable code we must ensure that the test cases are exhaustive,  
and have not missed any single corner of the feature/functionality

We need to set up any simple maven project in Eclipse or IDE of our choice and use the below code:  

**`App.java`** –  

```java
package com.thecodecache.code_coverage;

/**
 * Class under CodeCoverage
 * 
 * @author manoranjan.kumar
 */
public class App {

	public boolean isPalindrome(String input) {

		if (input == null) {
			throw new IllegalArgumentException("input shouldn't be null");
		}
		if (input.equals(reverse(input))) {
			return true;
		}

		return false;
	}

	/**
	 * just for the illustration purpose
	 * 
	 * just a plain simple function, not a sophisticated one,
	 * 
	 * @param input
	 * @return
	 */
	private String reverse(String input) {
		String reverse = "";
		for (int i = input.length() - 1; i >= 0; i--) {
			reverse += input.charAt(i);
		}
		return reverse;
	}

	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```

**AppTest.java** –  

```java
package com.thecodecache.code_coverage;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

/**
 * Unit test for simple App.
 */
public class AppTest {

	App app = new App();

	@Test
	public void isPalindromeSuccessTest() {
		assertEquals(true, app.isPalindrome("malayalam"));
	}

	@Test
	public void isPalindromeFailureTest() {
		assertEquals(false, app.isPalindrome("abcd"));
	}
}
```

**`pom.xml`** –  

```java
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.thecodecache</groupId>
    <artifactId>code-coverage</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <name>code-coverage</name>
    <!-- FIXME change it to the project's website -->
    <url>https://github.com/TheCodeCache/Java/edit/master/Code%20Coverage.md</url>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
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

# JaCoCo Report –  

- **High Level Summary** –  
  
  ![image](https://user-images.githubusercontent.com/26399543/153256933-2fc2346e-bc31-42cd-90a9-50af9b746871.png)  

- **Code Level Coverage** –  
  
  ![image](https://user-images.githubusercontent.com/26399543/153256727-3af1fc23-3adc-4360-808a-ed62eba50c91.png)  
