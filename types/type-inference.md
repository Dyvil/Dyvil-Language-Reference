---
dyvil: v0.31.0
---

# Type Inference

Dyvil supports type inference for members of kind `var`, `let`, `const` and `func`.

```swift
const s = "a" // s: String
func charCount(s: String) = s.length // charCount(s: String) -> int 
var i = charCount(s) // i: int
let a = [s, i] // a: [String | int]
```

This also works for other types such as generic types, tuples or functions.

```swift
let list  = List(1, 2, 3)                // List<int>
let fun   = (s: String) => s.toUpperCase // String -> String
let tuple = (1, "a")                     // (int, String)
```

## Local Type Inference

Unlike other functional programming languages like Haskell, the type inference in Dyvil is local. This means that type inference only flows in one direction:

```java
func myMethod(i, j) = i + j // invalid, i and j require explicit type
```

An advanced functional programming language could infer the types of the parameters `i` and `j`: a numeric type that supports the `+` operation.

However, Dyvil requires you to explicitly declare the type of the method parameters:

```java
func myMethod(i: int, j: int) = i + j
```

While the return type can be inferred to `int`, it is recommended for `public` API methods to explicitly declare their return type without relying on type inference.

