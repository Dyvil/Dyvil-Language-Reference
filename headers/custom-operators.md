# Custom Operators

Custom Operators can be defined in Header Files or in the header of a class file. Note that it is not possible to define custom operators anywhere else.

## Syntax

The following syntax is used to define a custom operator:

1. The type of operator
    - `infix`
    - `prefix`
    - `postfix`
2. The keyword `operator`
3. The name
4. An optional list of additional comma-separated properties in curly brackets.
    - `precedence` + integer literal
    - `associativity`
        - `none`
        - `left`
        - `right`

Example:

```swift
prefix operator  &
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

The order in which the properties are placed within the brackets does not matter.

## Precedence

The **Precedence** of an infix operator defines the order in which different operators are applied. The operator with the highest precedence value is always applied first. For example, an expression

```java
10 + 2 * 3
```

is de-sugared to

```java
10.+(2.*(3))
```

because the `*` operator has a higher precedence than the `+` operator.

### Prefix and Postfix Operators

By default, prefix and postfix operators have an infinite precedence, which means they are always applied first.

```java
   - 10  + 20
= (- 10) + 20
= 10
```

The order in which they are applied depends on the order in which they were placed in the source code. Prefix operators are applied from right to left while postfix operator are applied from left to right.

However, it is possible to define custom a custom precedence for these operators:


```swift
prefix operator println { precedence 10 }
```

This will allow you to type expressions like the following:

```java
println "hello " + "world"
println 10 + 10 + 22
```

Because the prefix operator `println` has a lower precedence than the `+` operator, the latter is applied first:

```java
println("hello " + "world")
println(10 + 10 + 22)
```

Without the custom precedence, the expression would evaluate to this:

```java
(println "hello ") + "world"
(println 10) + 10 + 22
```

The `println` doesn't return a result, so the compiler would give you an error without the custom precedence.

## Associativity

The **Associativity** of an infix operator is either `none`, `left` or `right`, and is the first value inside the curly brackets for infix operator declarations. It describes how the parser should handle expressions the same operator is applied directly after itself, as shown below

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