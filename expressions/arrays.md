# Arrays

Arrays are special values that can store multiple other values at once. They use the following syntax:

```swift
[ ] // empty array
[ value1, value2, ... ]
```

Where `value1`, `value2`, ... can be any expression, including other array expressions.

The implicit type of an array expression is determined according to the following algorithm:

1. If the array expression is empty, the type is `[any]`.
2. Otherwise, the type is `[type of value1 | type of value2 | ...]`, where `|` is the type union operator.