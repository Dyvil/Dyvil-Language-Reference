---
dyvil: v0.31.0
---

# Other Literals

## Booleans

Boolean Literals are the easiest to understand: There is only `true` and `false`. The integer equivalents for these are `1` \(or anything that is not `0`\) for `true` and `0` for `false`.

The type of Boolean Literals is always inferred to `boolean`.

## Null

The Null Literal `null` behaves exactly the same as in Java. It can be used in placed of any Nullable Type.

```swift
let obj: Object? = null
let string: String! = null
let dates: [Date]? = null
let array: [int]! = null
let i: int = null // error - int is a primitive type
```

The type of the Null Literal is inferred to the Null Type, which uses the same keyword.

```swift
var n = null
// becomes
var n: null = null
```

Note that it is not possible to assign anything other than `null` to such a variable. Thus, the compiler will reject the following code:

```swift
var n = null // n: null
n = "abc" // error - cannot assign java.lang.String to null
```

## Wildcard

Another special Literal Value is the Wildcard Literal `_`. It can be used in places where you want the default value of a type to be passed. The following table shows which value the Wildcard Literal will represent based on the type:

| Type | Value |
| --- | --- |
| `byte`, `short`, `char`, `int`, `long` | `0` |
| `float`, `double` | `0.0` |
| `boolean` | `false` |
| Any Nullable Type | `null` |

Because the value of the Wildcard Literal depends on the context, it's type cannot be inferred. Any attempt to do so will result in a compilation error. Since non-primitive non-nullable values cannot have a default value, it is a compile-time error to assign a wildcard literal to such a type.

