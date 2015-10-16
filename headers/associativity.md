# Associativity

The **Associativity** of an infix operator can be either `none`, `left` or `right`. It describes how the parser should handle expressions in which the same operator is applied multiple times.

```swift
infix operator +- { associativity none, precedence 120 }
//                                ^^^^
10 +- 20 +- 30
```

Depending on the `associativity`, the expression can be evaluated in different ways:

| Associativity | Desugared Expression |
|---------------|----------------------|
| none          | *#error#*            |
| left          | `10.+-(20).+-(30)`   |
| right         | `10.+-(20.+-(30))`   |

If the associativity of the `+-` operator is set to `none`, an expression like the above is not allowed, and parenthesis have to be placed explicitly. Otherwise, the compiler will cause a Syntax Error.

It is not possible to assign an associativity to prefix or postfix operators.