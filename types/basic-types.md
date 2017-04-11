---
dyvil: v0.31.0
---

# Basic Types

## The top type: `any`

Since there is no real super type of reference types and primitive types in the JVM, `any` is the semantic equivalent of `java.lang.Object`. That implies that boxing is required to correctly support primitive values. An variable such as

```swift
let a: any = 10
```

gets converted to the Java equivalent, which requires boxing to the `java.lang.Integer` class:

```java
Object a = Integer.valueOf(10)
```

## The bottom type: `none`

Similar to how `any` is the super-type of every other type, `none` is the sub-type of every type. An expression of type `none` can thus be assigned to any other type. Every `throw` statement has this type, and functions that always throw an exception or error can also use it to indicate this property.

```swift
func error() -> none = throw new Error()

var i: int = 10
i = error() // valid

var s: String = error() // valid
```

## The null type: `null`

When the compiler tries to infer the type of an expression that evaluates to `null` during compile-time \(usually `null` itself\), the `null` type gets inferred. For example, a variable such as

```java
var n = null
```

Gets inferred to:

```java
var n: null = null
```

Since the only value that is compatible with the `null` type is `null` itself, it is not possible to assign any other value to the variable `n`.

```java
n = "a" // compilation error - incompatible types
```

You can use `null` as the parameter or return type of a function. Expressions of type `null` can be assigned to Optional or Implicitly Unwrapped Optional Types:

```swift
var value: String? = null

func action() -> null { ...; null }

value = action()
```

## The Unit Type: `void`

The Unit Type `void` is a special data type in Java and Dyvil that is used to indicate that a function returns no value. It cannot be used as the type of a parameter, field or property.

```swift
func action() -> void { ... }

let a = action() // invalid - inferred type 'void' cannot be used as a variable type

let v: void = ??? // invalid
```

## Primitive Data Types

The following primitive types are supported in Dyvil:

| Name | Bits / Bytes | Signed | Floating-Point | Wrapper Class |
| :--- | :--- | :--- | :--- | :--- |
| `boolean` | 1 / 1 | - | - | `java.lang.Boolean` |
| `byte` | 8 / 1 | yes | no | `java.lang.Byte` |
| `short` | 16 / 2 | yes | no | `java.lang.Short` |
| `char` | 16 / 2 | no | no | `java.lang.Character` |
| `int` | 32 / 4 | yes | no | `java.lang.Integer` |
| `long` | 64 / 8 | yes | no | `java.lang.Long` |
| `float` | 32 / 4 | yes | yes | `java.lang.Float` |
| `double` | 64 / 8 | yes | yes | `java.lang.Double` |

Primitive Types share the same properties as primitive types in Java. However, there is one important difference: They can be used as generic type arguments, such as `List<int>`. This is only syntactic sugar though, as it will be converted to `List<Int>` at runtime, thus not eliminating the need for boxed values.

