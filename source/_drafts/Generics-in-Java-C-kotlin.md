---
title: Generics in Java, C++, kotlin
date: 2025-03-20 15:35:50
tags:
---

## Generic class

```c++
template<class T>
class vector {
    
}
```

- A is a subclass of B
- A ≤ B 
- A can be safely cast to B

f is a type transfromer

- f is **covariant** if A ≤ B → f(A) ≤ f(B)
- f is **contravariant** if A ≤ B → f(B) ≤ f(A)
- f is **invariant** if otherwise

Examples:

```java
class Fruit {}
class Apple extends Fruit {}
class Banada extends Fruit {}

class Pie<T> {
}

Pie<Apple> p1 = new Pie<Apple>();
Pie<Banada> p2 = new Pie<Banana>();

// Pie<T> -> () or Consumer<T> 

Consumer<Apple> action = eat;
Consumer<Fruit> j

eat(p1);
eat(p2);


public Pie<T> buy( T fruit ){} // T -> Pie<T> or Function<T, Pie<T>>

eat(p1);
eat(p2);



```


Dried<T> is invariant because Dried<Apple> ≤ Dried<Fruit>



```
