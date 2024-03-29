---
dyvil: v0.31.0
---

# Custom Operators

Custom Operators can be defined in Header Files or in the header of a class file. Note that it is not possible to define custom operators anywhere else.

The following syntax is used to define a custom operator:

1. The type of operator
   * `infix`
   * `prefix`
   * `postfix`
2. The keyword `operator`
3. The symbol
4. An secondary symbol for [ternary operators](ternary-operators.md) and [circumfix operators](../language-reference/operators/circumfix-operators.md) - only valid after `infix operator` or `prefix postfix operator`
5. An optional list of additional comma-separated properties within curly braces. Allowed properties:
   * `precedence` followed by an integer literal
   * `associativity` followed by one of
     * `none`
     * `left`
     * `right`

**Example**:

```swift
prefix  operator &
postfix operator ^
```

`infix` operators also need additional properties to be fully defined, namely a `precedence` value and an `associativity` type.

You can define these properties in curly brackets after the name of the operator:

```swift
infix operator +- { none,             120 }
//                  ^ associativity   ^ precedence
```

It is optional, but recommended for clarity, to type out which property is being defined:

```swift
infix operator +- { associativity none, precedence 120 }
infix operator +- { associativity none,            120 }
infix operator +- {               none, precedence 120 }
```

The order in which the properties are placed within the brackets does not matter. Duplicate properties are not permitted and will cause a diagnostic error.
