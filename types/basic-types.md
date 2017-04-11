# Basic Types

## The top type`any`

Since there is no real super type of reference types and primitive types in the JVM, `any` is the semantic equivalent of `java.lang.Object`. That implies that boxing is required to correctly support primitive values. An variable such as

```swift
let a: any = 10
```

gets converted to the Java equivalent, which requires boxing to the `java.lang.Integer` class:

```java
Object a = Integer.valueOf(10)
```

## The bottom type `none`

Similar to how `any` is the super-type of every other type, `none` is the sub-type of every type. An expression of type `none` can thus be assigned to any other type. Every `throw` statement has this type, and functions that always throw an exception or error can also use it to indicate this property.

## `null`, the type of the `null` literal

When the compiler tries to infer the type of an expression that evaluates to `null` during compile-time \(usually `null` itself\), the `null` type gets inferred. For example, a variable such as

```java
auto n = null
```

Gets inferred to:

```java
null n = null
```

Since the only value that is compatible with the `null` type is `null` itself, it is not possible to assign any other value to the variable `n`.

```java
n = "a" // compilation error - incompatible types
```

## Primitive Types

The following primitive types are supported in Dyvil:

| Name | Bits | Signed | Floating-Point |
| --- | --- | --- | --- |
| void | 0 | - | - |
| boolean | 1 \(8\) | - | - |
| byte | 8 | yes | no |
| short | 16 | yes | no |
| char | 16 | no | no |
| int | 32 | yes | no |
| long | 64 | yes | no |
| float | 32 | yes | yes |
| double | 64 | yes | yes |

Primitive Types share the same properties as primitive types in Java. However, there is one important difference: They can be used within generic type arguments, such as `List[int]`. This is only syntactic sugar though, as it will be converted to `List[Int]` at runtime, thus not eliminating the need for boxed values.

Boxed types for the primitive types can be found in the `dyvil.lang` package. They share the same name, although the first character is capitalized \(`Int`, `Boolean`, etc.\). The wrapper classes provide boxing and unboxing methods \(`apply` and `unapply`\) as well as all operator implementations \(`+`, `*`, `&`, `^`, ...\).

