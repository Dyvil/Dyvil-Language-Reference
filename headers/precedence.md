# Precedence

The **Precedence** of an infix operator defines the order in which different operators are applied. The operator with the highest precedence value is always applied first. For example, an expression

```java
10 + 2 * 3
```

is de-sugared to

```java
10.+(2.*(3))
```

because the `*` operator has a higher precedence than the `+` operator.

## Prefix and Postfix Operators

By default, prefix and postfix operators have an infinite precedence, which means they are always applied first.

```java
   - 10  + 20
= (- 10) + 20
= 10
```

The order in which they are applied depends on the order in which they were placed in the source code. Prefix operators are applied from right to left while postfix operator are applied from left to right.

However, it is possible to define custom a custom precedence for these operators:


```swift
prefix operator println { precedence 10 }
```

This will allow you to type expressions like the following:

```java
println "hello " + "world"
println 10 + 10 + 22
```

Because the prefix operator `println` has a lower precedence than the `+` operator, the latter is applied first:

```java
println("hello " + "world")
println(10 + 10 + 22)
```

Without the custom precedence, the expression would evaluate to this:

```java
(println "hello ") + "world"
(println 10) + 10 + 22
```

The `println` doesn't return a result, so the compiler would give you an error without the custom precedence.