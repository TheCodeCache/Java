# How to manipulate java byte-code:  

We can manipulate a given java source code files and translate/manipulate them into different versions.  
For ex:  
if we need to improve the code quality of the given source code programatically,  
then we may have to take the approach of manipulating the code at bytecode level.  

Code (**Input**):  
```java
class A {
    void test() {
        int b = 0;
        int c = 1;
        b += c;
    }
    int a;
}
```
Code (**Output**):  
```java
class A {
    void test() {
        this.b = 0; // <= Local variable initialize replaced with field assignment
        this.c = 1; // <=
        b += c;
    }
    int a;
    int b;          // <= Synthetic field that replaces the original local variable
    int c;          // <=
}
```

**Reference:**  
1. http://janino-compiler.github.io/janino/#janino-as-a-code-manipulator
2. https://github.com/janino-compiler/janino/blob/master/janino/src/test/java/org/codehaus/janino/tests/AstTest.java#LC359

