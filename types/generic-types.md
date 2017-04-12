---
dyvil: v0.31.0
---

# Generic Types

Generic Types provide a way to make operations available on different types of objects without having to redefine them.

A method that gets the first element of a list can be written as follows, using a combination of Generic Types and Type Variable Types.

```swift
static func getFirst<T>(list: List<T>) -> T = list.get(0)

let list1: List<int>    = List(1, 2, 3, 4)
let list2: List<long>   = List(1L, 1000L, 1000000L, 1000000000L)
let list3: List<String> = List("a", "b", "c")

let i = getFirst(list1) // type inferred to int
let l = getFirst(list2) // type inferred to long
let s = getFirst(list3) // type inferred to String
```

The generic type `List<T>` allows any `List` to be passed, be it `List<String>` or `List<int>`, and adapts the return type of the method accordingly.  
The type `List` can be parameterized with another type because it was defined as

```java
interface List<T> extends Collection<T>
```

Similarly, the type `Map<K, V>` can be used with two parameters, for example as `Map<Date, Person>`.

```java
interface Map<K, V>
```

```swift
let map1: Map<String, int> = Map("a": 1, "b": 2)
let map2: Map<int, long>   = Map(1: 1000L, 2: 1000000L)
```

## Tuple Types

A specialization of Generic Types are Tuple Types. They represent the parameterized class `Tuple.OfX<T1, ..., TX>`, where `X` is the number of elements in the Tuple. For example, a variable

```swift
let tuple = (1, "a")
```

Gets its type inferred to be `(int, String)`, which is syntactic sugar for `dyvil.tuple.Tuple.Of2<int, String>`. Tuple Types are [covariant](/types/variance.md), which means that `(int, String)` is a subtype of `(any, any)`, and an expression of the former type can be used where the latter type is required:

```swift
let anyTuple: (any, any) = tuple // ok
```

As of Dyvil v0.31.0, Tuple Types and Expressions are limited to 20 elements.

## Function Types

Another specialization of Generic Types are Function Types. They represent syntactic sugar for parameterized `dyvil.function.Function.OfX<P1, ..., PX, R>` types, where `X` is the number of parameters. For example, the function type `(String, int) -> boolean` is syntactic sugar for `Function.Of2<String, int, boolean>`. The last type argument \(in this case `boolean`\) represents the return type of the function type.

As with Tuple Types and some Generic Types, Function Types also use [variance](/types/variance.md) annotations. This is shown in the declaration of `dyvil.function.Function.Of2`:

```java
interface Of2<-P1, -P2, +R>
```

The parameter types are contravariant instead of covariant. This inverts the subtyping relationship, and makes a `Function2<any, any, String>` a subtype of `Function2<String, String, any>`.



