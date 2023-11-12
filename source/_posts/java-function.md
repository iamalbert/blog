---
title: Limitation of Java Lambdas
date: Sat Sep 7 17:42:06 EST 2023
categories:
    - programming
tags:
    - java
---


"First-class citizen" function means a function can be dynamically created and be passed around just like any other value. Java 8 added lambda expression that provide  "similar" feature by simplifying the creation of anonymous classes.


# Java Lambdas

Compared to other languages like JavaScript, Python, and C++, Java lambda expressions come with several limitations:

- **You can't use bound variables** (e.g., captured variables in C++ or upvalues in Lua) unless they are declared as `final`. Therefore, it's not easy to make closure or higher-order functions.
- **You can't throw checked exceptions**, unless the caller explicitly allows.

As lambda expressions are compiled as instantiating an anonymous class, apparently the compiler needs to figure out the name of the interface (of the anonymous class), and that interface must have exactly one abstract method. This leads to the most annoying limitation of Java lambdas: **Lambda expression must have an explicit target-type of `FunctionalInterface`**. 

In other languages, you can easily create an anonymous generic function.

```py
# Python
add = lambda x, y: x + y 

add(1, 2) # returns 3
add(1.0, 2.0) # returns 3.0
add('a', 'b') # returns 'ab'
```

```js
const add = (x, y) => x + y;

add(1, 2) # returns 3
add(1.0, 2.0) # returns 3.0
add('a', 'b') # returns 'ab'
```

```c++
// C++14
auto add = [](auto x, auto y){ return x + y;};

add(1, 2); // returns int(3) 
add(1.0, 2.0) // returns double(3.0)
add("foo"s, "bar"s); // returns string("foobar")
```

But in Java you simply can't do so. **Compiler is unable to infer the type of lambda expression**. It must be specified during declaration. This is probably the only case where a value is not convertible to `Object`, even `var` does not work here.

```java 
Object add = (x,y) -> x + y; 
// error: incompatible types: Object is not a functional interface

var add = (x,y) -> x + y;
// error: cannot infer type for local variable add
```

Users have to associate lambda expression with the correct interface so as to inform the compiler the number and types of the arguments and the type of the return value. Standard library kindly provides a few frequently-used [functional interfaces](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) to pick from.

```java 
BiFunction<Integer, Integer, Integer> addInteger = (x,y) -> x+y;
BiFunction<String, String, String> addString = (x,y) -> x+y; 
```

**You have to enumerate all arguments for lambda types not in the standard library**. For example, to represents a function that accepts four arguments and produces one result, you have to declare the corresponding interface first.

```java
public interface QuadFunction <T1, T2, T3, T4, R> {
    R apply(T1 t1, T2 t2, T3 t3, T4 t4);
};

QuadFunction<String, String, String, String, String> qf = (a,b,c,d)->a+b+c+d;
```

Just think how tedious it could be when there are many arguments.


On the other hand, **it is a compile-error to convert a lambda into a different functional interface**, even if they represent the same function. For example, a function taking one integer and returning a boolean, can be represented as
`Function<Integer, Boolean>` or `Predicate<Integer>`. But unfortunately these two types are not compatible with each other, because they have different names of their abstract methods.

```java 
Function<Integer, Boolean> isZero = x -> x != 0;
Predicate<Integer> isZero2 = isZero; 
// error: incompatible types: Function<Integer,Boolean> cannot be converted to Predicate<Integer>

Supplier<Child> makeObject = () -> new Child();
Supplier<Parent> makeObject2 = makeObject;
// error: incompatible types: Supplier<Child> cannot be converted to Supplier<Parent>

```




# Defined Interfaces in `java.util.function`

| Signature           | Name                  | Method   | Comment        |
| ------------------- | --------------------- | -------- | -------------- |
| `T      -> R`       | `Function<T, R>`      | `apply`  |                |
| `()     -> R`       | `Supplier<R>`         | `get`    |                |
| `T      -> boolean` | `Predicate<T>`        | `test`   |                |
| `T      -> Void`    | `Consumer<T>`         | `accept` |                |
| `T      -> T`       | `UnaryOperator<T>`    | `apply`  |                |
| `(T, U) -> R`       | `BiFunction<T, U, R>` | `apply`  |                |
| `(T, U) -> boolean` | `BiPredicate<T, U>`   | `test`   |                |
| `(T, U) -> Void`    | `BiConsumer<T, U>`    | `apply`  |                |
| `(T, T) -> T`       | `BinaryOperator<T>`   | `apply`  |                |
| `()     -> Void`    | `Runnable`            | `run`    | in `java.lang` |

# Custom functional interfaces

A functional interface must have *exactly one* non-overriding abstract method.


```java
public interface X1 {
    void func();
};

public interface X2 {
    void func();

    int number(){
        return 1;
    }
};

@FunctionalInterface
public interface X3 {
    void func();

    @Override
    String toString(); // This means X3 supertype already has a default implementation
};


@FunctionalInterface
public interface X4 {
    void func();
}
```


Apply `java.lang.FunctionalInterface` annotation so that compiler could check if the interface meets the criteria.

```java
@FunctionalInterface
public interface X5 {
    void func1();
    void func2();
} 
/*
|  Error:
|  Unexpected @FunctionalInterface annotation
|    X5 is not a functional interface
|      multiple non-overriding abstract methods found in interface X5
|  @FunctionalInterface
*/
```
