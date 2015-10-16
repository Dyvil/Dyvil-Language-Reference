# Type Aliases

Type Aliases allow you to define named aliases for complex types using a simple syntax:

```scala
type IntList = List[int]
type HashListMapping = Map[List[Map[_, long]], _]
```

The newly defined types can be used anywhere in the scope in which the Type Alias is available:

`MyClassA.dyv`:
```java
type IntList = List[int]

public header MyClassA

public class MyClassA
{
    IntList ints = [ 1, 2, 3 ]
    List[int] list = ints      // valid - same underlying type
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