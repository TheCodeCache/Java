# Code Analysis – 

**Note: Source Code Analysis could also be done by [`SonarQube`](https://www.sonarqube.org/)**

We can do static code analysis for any java class.  
`Static Code Analysis` is nothing but to know all about a java program (like java specific details, or code structural details)  
Using which we can produce neat code metrices and create custom style checking tools on top of it.  

**Maven Dependency** –  

```xml
<!-- https://mvnrepository.com/artifact/org.codehaus.janino/janino -->
<dependency>
    <groupId>org.codehaus.janino</groupId>
    <artifactId>janino</artifactId>
    <version>3.1.6</version>
</dependency>
```

Based on the AST ("abstract syntax tree") produced by the parser,  
the Traverser walks through all nodes of the AST,  
and derived classes can do all kinds of analyses on them, e.g. count declarations:

**Example:**  
```java
C:\Users\manoranjan.kumar> java org.codehaus.janino.samples.DeclarationCounter DeclarationCounter.java
Class declarations:     1
Interface declarations: 0
Fields:                 4
Local variables:        4
C:\Users\manoranjan.kumar>
```
This is the basis for all these neat code metrics and style checking  

# Janino – 

`Janino` is a very small, extremely fast open source Java compiler (Janino is a super-small, super-fast Java™ compiler).  
`Janino` can not only 
- compile Java source code files into bytecode files like `javac`,  

but also  
- compile Java expressions, blocks, classes and source code files in memory 
- load bytecodes and execute them directly in the JVM.  
`Janino` can also be used for **`static code analysis`** and **`code manipulation`**  

**Reference:**  
1. http://janino-compiler.github.io/janino/#janino-as-a-code-analyser
2. https://blog.karatos.in/a?ID=01700-c615febf-7f4e-48d9-ab5d-e58da905ef4e

