# Advanced Types

## Type Variable Types

Type Variable Types are simply references to Type Variables. Their subtyping behavior is defined by the variance annotations of the type variable. This means for a type variable:

```
T <: Number
```

A type variable reference `T` only accepts types that are subtypes of `Number`. If the type variable is unbounded, type variable types accept any type.

The most important use of Type Variable Types is type inference within methods. For example, the method in the example adapts its return type depending on the inferred type of the type variable type:

```java
static List[T] listOne(T element) = [ element ]

auto list = listOne("a") // list has the type 'List[String]' because 'T' was inferred to 'String'
```

## Wildcard Types

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

