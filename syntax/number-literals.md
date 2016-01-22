# Number Literals

As with comments, Dyvil also mostly inherits the syntax for number literals from Java.

## Integers

Integer literals are the most basic type of number literals. There are four types for different bases available, all of which are indicated with different prefixes.

| Prefix | Base | Digit Range (inclusive) | Examples |
| ------ | ---- | -------- |
| none   | 10   | 0 - 9 | `123`, `1000`, `007` |
| `0b`   | 2    | 0 - 1 | `0b1001`, `0b0011` |
| `0o`   | 8    | 0 - 7 | `0o777`, `0o0123` |
| `0x`   | 16   | 0 - F | `0x123`, `0xABCDEF`, `0xDEADBEEF` |

- All sorts can have as many leading zeros (after the prefix) as necessary.
- Leading minus signs `-` are not part of the tokens. They are always handled specially by the parser.
- Base-16 'digits' `A` - `F` can also be lowercase `a` - `f`.

Integer Literals can only be in the range $$-2^{32}$$ to $$2^{32}-1$$. Otherwise, the compiler or REPL will cause a syntax error. For a greater range of values, Long Literals have to be used.

For integer literals, the primitive type `int` is inferred.

## Longs

Long Literals work much like integer literals. However, they have to be disambiguated by adding a trailing `l` or `L`.

```java
10L
10000000000000l
0xFFFFFFFFFFFFL
0b10101001011010110011010110101100110L
```

Long Literals allow a range of values from $$-2^{64}$$ to $$2^{64}-1$$.

Both Integer and Long Literals may have an arbitrary number of underscores `_` in between digits to increase readability.

```java
1_000_000
0xFF_AA_BB_EE
```

## Floating-Point Literals

Floating Point Literals can be used to express numbers with decimal places. Unlike Integer Literals, they are only available as base-10 and base-16 literals.

```java
10.5
123.456
0.125
1.0
0x1A.3F // base-16
```

It is also possible to add an exponent to floating point literals:

```java
1.5e4 -> 1500.0
0.3e-2 -> 0.003
0.4e10 -> 4000000000.0
```

Valid Floating-Point Literals cannot start or end with a period symbol `.`. Thus, the following expressions are illegal in Dyvil:

```java
.25
.50
.123456
1.
```

Without a `F` or `D` postfix to explicitly declare it, the type of floating point literals will be inferred as `double`. However, it is recommended to always add the postfix characters for clarity.

### Float Literals

Float Literals can be created by suffixing a normal Floating-Point Literal with an `f` or `F`. This will treat the literal as a `float` value and will infer that type for the literal.

```java
2F
1.5F
0.3f
2.5e4f
```

### Double Literals

Double Literals are Floating-Point-Literals suffixed with a `d` or `D` character. Their type will then be inferred to `double`.

```java
10D
1.000001d
2e-3D
4.5e12d
```