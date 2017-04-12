---
dyvil: v0.31.0
---

# Variance

Depending on the variance of the type variables in a class declaration, Generic Types can have different subtyping relationships.

## Invariance

The most common variance is Invariance. It is declared by leaving out any variance annotations in Type Parameter declarations. For example, the `List[T]` class is defined as

```java
interface List<T> extends Collection<T>
```

Because of the missing variance annotation, the `List` type is invariant. This means the following fails:

```java
class A
class B extends A

let listB: List<B> = ...
let listA: List<A> = listB // error: incompatible types
```

The reason for this is that although `B` is a sub-type of `A`, `List<B>` is not a sub-type of `List<A>`.

## Covariance

The second type of variance is Covariance. It declares that if a generic type `C<T>` is a sub-type of `C<S>` if `T` is a sub-type of `S`. A common example for this is the `Tuple.Of2` class:

The tuple class `dyvil.tuple.Tuple.Of2` is defined as

```scala
class Of2<+T, +U>
```

The type variables `A` and `B` are both covariant, as denoted by the `+` variance annotation. This defines the subtyping relation for the parameterized type `Tuple.Of2` as follows \(the syntax `(T, U)` is equivalent to `Tuple.Of2<T, U>`\):

```swift
(T, U) <: (X, Y) if T <: X && U <: Y
```

Example:

```swift
let tupleBB: (B, B) = ...
let tupleAB: (A, B) = tupleBB // fine!
let tupleBA: (B, A) = tupleBB // fine!
let tupleAA: (A, A) = tupleBB // fine!
// however:
tupleBA = tupleAB // error: A is not a sub-type of B
```

## Contravariance

The third variance type and opposite of Covariance is Contravariance. It is denoted by a `-` minus sign before the Type Parameter.

```java
interface Function<-T, +U>
```

The subtyping relationship of contravariant generics is exactly the opposite of that of covariant ones. A generic type `C[T]` is a sub-type of `C[S]` if `S` is a **sub**-type of `T` \(the syntax `T -> U` is equivalent to `Function.Of1<T, U>`\)

```swift
(T -> U) <: (X -> Y) if T >: X && U <: Y
```

Example:

```swift
let functionBB: B -> B = ...
let functionAB: A -> B = functionBB // error: B is not a super-type of A
let functionBA: B -> A = functionBB // error: A is not a sub-type of B (covariant!)
let functionAA: A -> A = functionBB // error: s.a.
// but:
functionBB = functionAB // fine: A is a super-type of B
```

The last example can be explained like this: A function that can take an `A` parameter could also handle a `B` parameter. Thus, the `functionAB` can be used in place of `functionBB`.

