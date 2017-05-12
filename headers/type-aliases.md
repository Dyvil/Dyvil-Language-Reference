---
dyvil: v0.32.0
---

# Type Aliases

Type Aliases allow you to define named aliases for complex types using a simple syntax:

```scala
type IntList = List<int>
type HashListMapping = Map<List<Map<_, long>>, _>
```

The newly defined types can be used anywhere in the scope in which the Type Alias is available:

`MyClassA.dyv`:

```swift
type IntList = List<int>

header MyClassA

class MyClassA
{
    let ints: IntList = [ 1, 2, 3 ]
    let list: List<int> = ints      // valid - same underlying type
}
```

When defined in headers or classes with Header Declarations, Type Aliases are also available through Include Declarations:

`MyClassB.dyv`

```swift
using MyClassA

class MyClassB
{
    let ints: IntList = List(1, 10, 100)
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

let f: Func<int> = () => 1
// (() -> int) f = ...
let l: Func<String, int> = s => s.length
// (String -> int) l = ...
let c: Func<String, String, String> = (s1, s2) => s1 + s2
// ((String, String) -> String) c = ...
```



