# Type Inference

Dyvil supports type inference using the special keyword `auto`.

```java
auto i = "a".length
```

The compiler will first determine the type of the value, which resolves to the type of the method `java.lang.String#length()int`, which has the return type `int`. Then, the type will be inferred to the variable, making it

```java
int i = "a".length
```

This also works for other types such as generic types, tuples or functions.

```java
auto list = List(1, 2, 3)              // List[Int]
auto fun = (String s) => s.toUpperCase // String => String
auto tuple = (1, "a")                  // (int, String)
```

## Local Type Inference

Unlike other functional programming languages like Haskell, the type inference in Dyvil is local. This means that type inference only flows in one direction:

```java
auto myMethod(auto i, auto j) = i + j
```

An advanced functional programming language could infer the types of the parameters `i` and `j`: a numeric type that supports the `+` operation.

However, Dyvil requires you to explicitly declare the type of the method parameters:

```java
auto myMethod(int i, int j) = i + j
```

While the return type can be inferred to `int`, this is not recommended for `public` API methods.

