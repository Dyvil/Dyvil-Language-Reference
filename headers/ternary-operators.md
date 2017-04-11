---
dyvil: v0.31.0
---

# Ternary Operators

Ternary Operators are a special form of infix operators that have three operands and two operators. They can be declared by adding a second symbol to an `infix operator` declaration:

```swift
infix operator ? : { precedence 100 }
```

While ternary operators can define a `precedence`, they may not have an `associativity` attribute. The associativity  can be viewed as if it was `left` for the first operator and `right`  for the second operator. The following example illustrates how ternary operator expressions are grouped:

```swift
 a | b  ?  c + d  :  e * f
(a | b) ? (c + d) : (e * f)

a ?  b ? c : d  : e
a ? (b ? c : d) : e

a ? b : c ? d : e
a ? b : (c ? d : e)
```

While the standard library only defines the Ternary Conditional Operator `? :`, you can define your own custom ternary operators with any two symbols.

