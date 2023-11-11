---
title: Java functional interface
categories:
    - Programming
tags:
    - java
---

## Defined Interfaces in `java.util.function`

| Signature          | Name                 |  Method 
|--------------------|----------------------|------------- 
| ()     -> R        |  Supplier<R>         |  get      
|                    |                      |
| T      -> R        |  Function<T, R>      |  apply
| T      -> boolean  |  Predicate<T>        |  test
| T      -> Void     |  Consumer<T>         |  accept
| T      -> T        |  UnaryOperator<T>    |  apply
|                    |                      |
| (T, U) -> R        |  BiFunction<T, U, R> |  apply
| (T, U) -> boolean  |  BiPredicate<T, U>   |  test
| (T, U) -> Void     |  BiConsumer<T, U>    |  apply
| (T, T) -> T        |  BinaryOperator<T>   |  apply
|                    |                      |
| ()     -> Void     |  java.lang.Runnable  |  run

## Custom Functional interfaces

1. Interface must have exactly one non-overriding abstract method.


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
    String toString();
};


@FunctionalInterface
public interface X4 {
    void func();
}
```


2. Use `java.lang.FunctionalInterface` annotation so that compiler check if it matches the criteria.

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
