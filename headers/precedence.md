---
dyvil: v0.31.0
---

# Precedence

The **Precedence** of an infix operator defines the order in which different operators are applied. The operator with the highest precedence value is always applied first. For example, an expression

```java
10 + 2 * 3
```

is de-sugared to

```java
10 + (2 * 3)
```

because the `*` operator has a higher precedence than the `+` operator.

## Prefix and Postfix Operators

Prefix and postfix operators have an infinite precedence against infix operators. This means they are always applied first.

```java
   - 10  + 20
= (- 10) + 20
= 10
```

The order in which they are applied depends on the order in which they were placed in the source code. `Prefix` operators are applied from right to left while `postfix` operator are applied from left to right. Postfix operators have a higher precedence than prefix operators.

```swift
- -  10 ! !
- -((10 !) !)
-(-((10 !) !))
```



