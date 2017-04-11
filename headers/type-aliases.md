---
dyvil: v0.31.0
---

# Type Aliases

Type Aliases allow you to define named aliases for complex types using a simple syntax:

```scala
type IntList = List<int>
type HashListMapping = Map<List<Map<_, long>>, _>
```

The newly defined types can be used anywhere in the scope in which the Type Alias is available:

`MyClassA.dyv`:

```java
type IntList = List<int>

public header MyClassA

public class MyClassA
{
    let ints: IntList = [ 1, 2, 3 ]
    let list: List<int> = ints      // valid - same underlying type
}
```

When defined in headers or classes with Header Declarations, Type Aliases are also available through Include Declarations:

`MyClassB.dyv`

```java
include MyClassA

public class MyClassB
{
    IntList ints = List(1, 10, 100)
}
```

## Generic Type Aliases

You can make a generic Type Aliases that takes a few input type parameters to customize the resulting type. This is done using the usual generic syntax:

```swift
type NestedList<T> = List<List<T>>
```

When using this Type Alias, all occurrences of the type parameter will be replaced with the argument. This is shown below, where the type argument is `int`:

```swift
let list: NestedList<int> = []
// expands to
let list: List<List<int>> = []
```

Generic Type Aliases can also be overloaded by arity. This example implements a C\#-style Function Type style:

```swift
type Func<R> = () -> R
type Func<P1, R> = P1 -> R
type Func<P1, P2, R> = (P1, P2) -> R
// ...

Func<int> f = () => 1
// (() -> int) f = ...
Func<String, int> l = s => s.length
// (String -> int) l = ...
Func<String, String, String> c = (s1, s2) => s1 + s2
// ((String, String) -> String) c = ...
```



