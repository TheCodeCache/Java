# org.codehause.janino

Janino is a super-small, super-fast Java compiler.  

Janino can not only `compile` a set of `source files` to a set of `class files` like `JAVAC`,  
but also 
- compile a `Java expression`
- a `block`
- a `class body`
- one `.java file`
- a `set of .java files` in memory,  
load the bytecode and execute it directly in the same JVM.  

Let's say we build an e-commerce system, which computes the shipping cost for the items that the user put into his/her shopping cart.  
Because we don't know the merchant's shipping cost model at implementation time,  
we could implement a set of shipping cost models that come to mind (flat charge, by weight, by number of items, ...) and select one of those at run-time.  

In practice, we will most certainly find that the shipping cost models we implemented will rarely match what the merchant wants,  
so we must add custom models, which are merchant-specific.  
If the merchant's model changes later, we must change our code, re-compile and re-distribute our software.  

Because this is so unflexible, the shipping cost expression should be specified at run-time, not at compile-time.  
This implies that the expression must be scanned, parsed and evaluated at run-time, which is why we need an expression evaluator.  

**Important-**  
A simple expression evaluator would parse an expression and create a "syntax tree".  
The expression "a + b * c", for example,  
this would compile into a "Sum" object who's first operand is parameter "a" and who's second operand is a "Product" object who's operands are parameters "b" and "c".  
Such a syntax tree can evaluated relatively quickly.  
However, the run-time performance is about **`100 times slower`** than that of `"native"` Java code executed directly by the JVM.  
This limits the use of such an expression evaluator to simple applications.  

Also, we may want not only do simple arithmetics like "a + b * c % d",  
but take the concept further and have a real "scripting" language which adds flexibility to our application.  
Since we know the Java programming language already,  
we may want to have a syntax that is similar to that of the Java programming language.  

Compiling Java programs with ORACLE's JDK is a relatively resource-intensive process (disk access, CPU time, ...).  
This is where Janino comes into play... a `light-weight`, `embedded` Java compiler,  
that compiles simple programs in memory into JVM bytecode which executes within the JVM of the running program.  

**Reference:**  
1. http://janino-compiler.github.io/janino/#basic-examples
2. https://mvnrepository.com/artifact/org.codehaus.janino
