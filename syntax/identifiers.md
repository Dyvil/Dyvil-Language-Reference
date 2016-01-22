# Identifiers

The rules for identifiers in Dyvil are much more tolerant than in Java. Dyvil differentiates between two different types of identifiers:

## Alphanumeric Identifiers

Alphanumeric Identifiers are the identifiers made of lower- and uppercase letters and digits. They can also be built from Unicode characters.

**Examples**:
```java
identifier
id10
name
MyClassName
áccent
λάμδα
```

The first character in alphanumeric identifiers must not be a digit.

## Symbols Identifiers

Symbols Identifiers are, as the name suggests, made of mathematical or other (Unicode) symbols. In the language, they are usually used and interpreted as operators. It is possible to create symbol identifiers with period symbols `.` in any position, but the symbol alone is not a valid identifier.

**Examples**:
```java
++
+-+-+
*##+*
^-^
%&/!!
\=
..
..<
.*
±
÷
—÷
≥≤
```

## Combining Alphanumeric and Symbol Identifiers

Alphanumeric and Symbols Identifiers cannot be directly combined without special symbols. For example, the text

```java
name*=
```

Produces two identifier tokens, `name` and `*=` separately. However, it is possible to create a single identifier that consists of both alphanumeric and mathematical symbols. This can be achieved by separating them with either an underscore `_` or a dollar sign `$`.

```java
subcript_=
=$eq
```

Note that a single underscore is not a valid identifier, while a single dollar sign is.

As per symbol substitution described in [Operators](headers/operators.md), the examples above can be de-sugared to

```java
subscript_$eq
$eq$eq
```

They way in which the identifiers are used (qualified or unqualified) is not considered. A method named `$eq$eq` can also be called with the `==` operator, because these two identifiers have the same underlying meaning.