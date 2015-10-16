# Custom Operators

## Operators in Dyvil

Headers are the only place where it is allowed to define custom Operators. This is due to the fact that they are used by the class-level parser and thus have to be declared first.

Through **Operators**, Dyvil provides a way to 1. override existing operators and 2. define new operators. In Dyvil, there is no clear distinction between an alphanumerical identifier such as `fooBar123` and an operator with symbols, for example `+`, `+:-` or `*\*`. That means one could easily name a method with an operator name without any problems, as shown below

```scala
infix int +-(int i, int j) = i + -j
1 +- 2 // -1
```

To be JVM-compatible, these names have to be replaced by the compiler according to the following table

| Symbol | Replacement |
|--------|-------------|
| =      | $eq         |
| +      | $plus       |
| -      | $minus      |
| *      | $times      |
| /      | $div        |
| \      | $bslash     |
| %      | $percent    |
| #      | $hash       |
| @      | $at         |
| <      | $lt         |
| >      | $gt         |
| :      | $colon      |
| .      | $dot        |
| !      | $bang       |
| ?      | $qmark      |
| ~      | $tilde      |
| ^      | $up         |
| &      | $amp        |
| $$|$$  | $bar        |

For example, an operator `+*` would be replaced with `$plus$times`.

## Custom Operators

Operator Definitions can be declared in Header Files or in the header of a class file with the type of the operator, the keyword `operator` and the name, optionally followed by additional properties for `infix` operators.

```swift
prefix operator &
postfix operator ^
```

`infix` operators also need additional properties to be fully defined, namely a `precedence` value and an `associativity` type.

```swift
infix operator +- { none,            120 }
                    ^ associativity  ^ precedence
```

## Associativity

The **Associativity** of an infix operator is either `none`, `left` or `right`, and is the first value inside the curly brackets for infix operator declarations. It describes how the parser should handle expressions the same operator is applied directly after itself, as shown below

```swift
infix operator +- { [associativity], 120 }
10 +- 20 +- 30
```

Depending on the `[associativity]`, the expression can be evaluated in different ways:

| Associativity | Desugared Expression |
|---------------|----------------------|
| none          | #error#              |
| left          | `10.+-(20).+-(30)`   |
| right         | `10.+-(20.+-(30))`   |

If the associativity of the `+-` operator is set to `none`, in expression like the above is disallowed, and parenthesis have to be placed explicitly. Otherwise, the compiler will cause a Syntax Error.

It is not possible to assign an associativity to prefix or postfix operators.

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
- 10 + 20 // becomes
(- 10) + 20
= 10
```

The order in which they are applied depends on the order in which they were placed in the source code. Prefix operators are applied from right to left while postfix operator are applied from left to right.

However, it is possible to define custom a custom precedence for these operators:


```java
prefix operator println { precedence 10 }
```

This will allow you to type expressions like the following:

```java
println "hello " + "world"
println 10 + 10 + 22
```

Because the prefix operator `println` has a lower precedence than the `+` operator, the latter is applied first:

```
println("hello " + "world")
println(10 + 10 + 22)
```

Without the custom precedence, the expression would evaluate to this:

```
(println "hello ") + "world"
(println 10) + 10 + 22
```

The `println` doesn't return a result, so the compiler would give you an error without the custom precedence.