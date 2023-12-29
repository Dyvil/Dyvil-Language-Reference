# Implementation

Operators are implemented with as static methods. They can be `prefix`, `infix`, `postfix`, and `static` methods. Here are some examples:

```swift
class MyOperators {
    // -i
    prefix func -(rhs: int) -> int = ...

    // i++
    postfix func ++(rhs: int^) -> int = ...

    // 2 ** 3
    infix func **(lhs: int, rhs: int) -> int = ...

    // |arr|
    static func |_|(array: [int]) -> int = ...
}
```
