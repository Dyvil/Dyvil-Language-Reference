---
dyvil: v0.31.0
---

# Special Types

## Type Variable Types

Type Variable Types are simply references to Type Variables. Their subtyping behavior is defined by the variance annotations of the type variable. This means for a type variable:

```
T <: Number
```

A type variable reference `T` only accepts types that are subtypes of `Number`. If the type variable is unbounded, type variable types accept any type.

The most important use of Type Variable Types is type inference within methods. For example, the method in the example adapts its return type depending on the inferred type of the type variable type:

```java
func listOf(element: T) -> List<T> = [ element ]

let list = listOne("a") // list has the type 'List<String>' because 'T' was inferred to 'String'
```

## Wildcard Types

Wildcard Types are a way to allow use-site variance, as opposed to [declaration-site variance](/types/variance.md). For example, since the type `List<T>` is invariant on `T`, a `List<String>` cannot be used in place of a `List<Object>`. However, this problem can be avoided using wildcard types:

```swift
let strings: List<String> = [ "a", "b", "c" ]
let objects: List<Object> = strings           // type error - List<String> is incompatible with List<Object>
// solution:
let objects: List<+Object> = strings          // List of 'something that is a subtype of' Object
```

The above example shows how Wildcard Types can be used for covariant subtyping problems. It is also possible to use them for contravariant problems:

```swift
let strings: List<-String> = objects   // List of 'anything that is a supertype of' String
```

In this example, `List<Object>` is compatible with `List<-String>` because `Object >: String`, i.e. `Object` is a super type of `String`.

The Wildcard Type `_` as in `List<_>` is equivalent to `+any!`. This means you can assign a list of any nullable or non-nullable type to a `List<_>`.

