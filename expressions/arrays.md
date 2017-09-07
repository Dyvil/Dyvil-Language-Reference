# Arrays

Arrays are special values that can store multiple other values at once. They use the following syntax:

```swift
[ ] // empty array
[ value1, value2, ... ]
```

Where `value1`, `value2`, ... can be any expression, including other array expressions.

The implicit type of an array expression is determined according to the following algorithm:

1. If the array expression is empty, the type is `[any]`.
2. Otherwise, the type is `[type of value1 | type of value2 | ...]`, where `|` is the [type union](/types/special-types.md) operator.

The example below shows how the type of different array expressions is inferred:

```swift
let e = [] // e: [any]
let i = [ 1, 2, 3 ] // i: [int]
let j = [ 1, "a", true ] // j: [int | String | boolean]
let k = [ 1, null ] // k: [int?]
```

If an explicit type is enforced, e.g. by using a cast or a type ascription, the array expression can automatically cast its subexpressions to the expected element type.

```swift
let e: [int] = [] // ok
let n: [[int]] = [[]] // ok

let f: [String] = [ 1 ] // not ok, cannot convert int to String

print n[0].dynamicClass // prints 'class [I', i.e. class<[int]>
```

Methods and operators that can be used with arrays are declared in the `dyvil.array.*Array` class corresponding to the element type. The most important operations are subscript, subscript assignment, and accessing the `size` property.

```swift
let a = [ 1, 2, 3 ]

print a.size // prints '3'
print a[0] // prints '1'

a[1] = 4
print a // prints [1, 4, 3]
```