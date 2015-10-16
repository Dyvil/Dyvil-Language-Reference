# Generic Types

Generic Types provide a way to make operations available on different types of objects without having to redefine them.

A method that gets the first element of a list can be written as follows, using a combination of Generic Types and Type Variable Types.

```java
static T getFirst[T](List[T] list) = list[0]

List[int] list1 = List(1, 2, 3, 4)
List[long] list2 = List(1L, 1000L, 1000000L, 1000000000L)
List[String] list3 = List("a", "b", "c")

auto i = getFirst(list1) // type inferred to int
auto l = getFirst(list2) // type inferred to long
auto s = getFirst(list3) // type inferred to String
```

The generic type `List[T]` allows any `List` to be passed, be it `List[String]` or `List[int]`, and adapts the return type of the method accordingly.
The type `List` can be parameterized with another type because it was defined as

```java
interface List[T] extends Collection[T]
```

Similarly, the type `Map[K, V]` can be used with two parameters, for example as `Map[Date, Person]`.

```java
interface Map[K, V]
```
```java
Map[String, int] map1 = Map("a" -> 1, "b" -> 2)
Map[int, long] map2 = Map(1 -> 1000L, 2 -> 1000000L)
```

## Variance

Depending on the variance of the type variables in a class declaration, Generic Types can have different subtyping relationships.

### Invariance

The most common variance is Invariance. It is declared by leaving out any variance annotations in Type Parameter declarations. For example, the `List[T]` class is defined as

```java
interface List[T] extends Collection[T]
```

Because of the missing variance annotation, the `List` type is invariant. This means the following fails:

```java
class A
class B extends A

List[B] listB = ...
List[A] listA = listB // error: incompatible types
```

The reason for this is that although `B` is a sub-type of `A`, `List[B]` is not a sub-type of `List[A]`.

### Covariance

The second type of variance is Covariance. It declares that if a generic type `C[T]` is a sub-type of `C[S]` if `T` is a sub-type of `S`. A common example for this is the `Tuple2` class:

The tuple class `dyvil.tuple.Tuple2` is defined as

```scala
class Tuple2[+T, +U]
```

The type variables `A` and `B` are both covariant, as denoted by the `+` variance annotation. This defines the subtyping relation between the parameterized type `Tuple2` as follows:

```
Tuple2[T, U] <: Tuple[X, Y] if T <: X and U <: Y
```

Example:

```java
Tuple2[B, B] tupleBB = ...
Tuple2[A, B] tupleAB = tupleBB // fine!
Tuple2[B, A] tupleBA = tupleBB // fine!
Tuple2[A, A] tupleAA = tupleBB // fine!
// however:
tupleBA = tupleAB // error: A is not a sub-type of B
```

### Contravariance

The third variance type and opposite of Covariance is Contravariance. It is denoted by a `-` minus sign before the Type Parameter.

```java
interface Function1[-T, +U]
```

The subtyping relationship of contravariant generics is exactly the opposite of that of covariant ones. A generic type `C[T]` is a sub-type of `C[S]` if `S` is a **sub**-type of `T`.

```
Function1[T, U] <: Function1[X, Y] if T >: X and U <: Y
```

Example:

```java
Function[B, B] functionBB = ...
Function[A, B] functionAB = functionBB // error: B is not a super-type of A
Function[B, A] functionBA = functionBB // error: A is not a sub-type of B (covariant!)
Function[A, A] functionAA = functionBB // error: s.a.
// but:
functionBB = functionAB // fine: A is a super-type of B
```

The last example can be explained like this: A function that can take an `A` parameter could also handle a `B` parameter. Thus, the `functionAB` can be used in place of `functionBB`.
