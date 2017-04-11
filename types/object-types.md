---
dyvil: v0.31.0
---

# Object Types

Object types are named references to existing non-generic types. They are, among generic types, the most commonly used types in Dyvil. An object type can consist of either a simple name or a qualified one. The former are resolved using declarations in the enclosing header and/or other classes in the same package.

## Examples

```swift
let s: String = "abc"
let o: Object = new Object
let i: Integer = 10

let b: java.lang.Boolean = false
let p: com.example.Person = Person(name: "Frank", age: 30)
```



