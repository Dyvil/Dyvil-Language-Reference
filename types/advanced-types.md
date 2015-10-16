# Advanced Types

## Tuple Types

A specialization of Generic Types are Tuple Types. They represent the parameterized class `TupleX[T1, ..., TX]`, where `X` is the number of elements in the Tuple. For example, a variable

```scala
var tuple = (1, "a")
```

gets its type inferred to be `(int, String)`, which is syntactic sugar for `dyvil.tuple.Tuple2[Int, String]`. Tuple Types are [[Covariant|Variance#Covariant]], which means that `(int, String)` is a subtype of `(any, any)`, and an expression of the former type can be used where the latter type is required

```scala
(any, any) tuple2 = tuple // ok
```

## Function Types

Another specialization of Generic Types are Function Types, which represent syntactic sugar for parameterized `dyvil.function.FunctionX` types, where `X` is the number of parameters. For example, the function type `(String, int) => boolean` is syntactic sugar for `Function2[String, Int, Boolean]`. The last type argument (in this case `Boolean`) represents the return type of the function type.

As with Tuple Types and some Generic Types, Function Types are also fitted with [[variance annotations |Variance]], as shown in the declaration of `dyvil.function.Function2`.

```scala
interface Function2[-P1, -P2, +R]
```

However, the parameter types are not covariant, but [[contravariant|Variance#Contravariance]]. This inverts the subtyping relationship, and makes a `Function2[any, any, String]` as subtype of `Function2[String, String, any]`.

## Type Variable Types

Type Variable Types are simply references to [[Type Variables]]. Their subtyping behavior is defined by the bounds of the type variable, which means for a type variable

```
T <: Number
```

A type variable reference `T` only accepts types that are subtypes of `Number`. If the type variable is unbounded, type variable types accept any type.

The most important use of Type Variable Types is type inference within methods. For example, a method

```java
static List[T] listOne(T element) = [ element ]
```

adapts its return type depending on the inferred type of the type variable type.

```scala
var list = listOne("a") // list has the type 'List[String]' because 'T' was inferred to 'String'
```

##Wildcard Types

Wildcard Types are a way to allow use-site variance, as opposed to [declaration-site variance](types/generic-types.md#Variance). For example, since the type `List[T]` is invariant on `T`, a `List[String]` cannot be used in place of a `List[Object]`. However, this problem can be avoided using wildcard types:

```java
List[String] strings = [ "a", "b", "c" ]
List[Object] objects = strings           // type error - List[String] is incompatible with List[Object]
// solution:
List[_ <: Object] objects = strings      // List of 'something that is a subtype of' Object
```

The above example shows how Wildcard Types can be used for covariant subtyping problems. However, it is also possible to do the same for contravariant problems:

```java
List[_ >: String] strings = objects   // List of 'something that is a supertype of' String
```

In this example, `List[Object]` is compatible with `List[_ >: String]` because `Object >: String`, i.e. `Object` is a super type of `String`.