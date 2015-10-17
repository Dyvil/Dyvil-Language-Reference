# Other Literals

## Boolean

Boolean Literals are the easiest to understand: There is only `true` and `false`. The integer equivalents for these are `1` (or anything that is not `0`) for `true` and `0` for `false`.

The type of Boolean Literals is always inferred to `boolean`.

## Null

The Null Literal `null` behaves exactly the same as in Java. It can be used in placed of any reference type, including arrays.

```java
Object obj = null
String string = null
[Date] dates = null
[int] array = null
int i = null // error!
```

The type of the Null Literal is inferred to the Null Type with the same notation.

```java
auto n = null
// becomes
null n = null
```

Note that it is not possible to assign anything other than `null` to such a variable.

## Nil

A new literal in Dyvil is the `nil` literal. It can be used for anything that has an empty state, such as arrays, `List`s or `Option`s.

```java
[int] ints = nil            // [] / [int] with length = 0
List[int] intList = nil     // [] / EmptyList
Option[String] option = nil // None
```

Note that the value of these variables is in no case `null`, but rather the corresponding "empty" implementations or containers.

The type of the `nil` literal cannot be inferred, as its value depends on the context in which it is used.

## Wildcard

Another special Value Literal is the Wildcard Literal `...`. It can be used in places where you the default value of a type to be passed. The following table shows which value the Wildcard Literal will represent based on the type:

| Type                                   | Value   |
| -------------------------------------- | ------- |
| `byte`, `short`, `char`, `int`, `long` | `0`     |
| `float`, `double`                      | `0.0`   |
| `boolean`                              | `false` |
| Any reference type                     | `null`  |

Because the value of the Wildcard Literal depends on the context, its type cannot be inferred. Any attempt to do so will result in a compilation error.