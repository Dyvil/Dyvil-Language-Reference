# String Literals

String Literals are a way to express text for use in programs. There are two types of String Literals, single-quoted and double-quoted ones, both of which have their own special semantics.

## Single-Quoted String Literals

Single-Quoted String Literals are indicated and terminated with a single quote `'`.

```java
'hello world'
'a'
'"Single-qouted strings can contain double-quotes", he said'
```

The type of Single-Quoted String Literals is inferred as `java.lang.String`. However, it is possible to use them as `char` literals by explicitly stating that this type is wanted:

```java
'a' as char
char c = 'C'
```

This is only possible if the Single-Quoted String consists of exactly one character (Unicode code-point).

## Double-Quoted String Literals

Double-Quoted String Literals are both started and ended with a double-quote symbol `"`. This means they cannot contain this character, for example for quotes within the text.

```java
"Hello World"
"a"
"'Double-quoted Strings can contain single-quotes', she said"
""this is not possible" - the compiler" // error
```

The type of Double-Quoted String Literals is always inferred as `java.lang.String`. Explicitly or implicitly casting to `char` causes a semantic error.

## Multi-line Rules

Both types of String Literals can span multiple lines by simply adding a newline in the body of the literal.

```java
"This is a multi-line
 string"
```

To avoid problems with indentation, tab characters are ignored in String Literals:

```java
class Test
{
    String s = "Hello, 
                World"
}
```

## Escape Characters

It is possible to insert certain special characters into String Literals via Escape Sequences. They are indicated by a backslash `\` followed by a single symbol. The symbol determines the character that is actually inserted into the String.

```java
char tab = '\t'
char cr = '\r'
```

The following table shows the escape sequences and the symbols that are actually inserted:

| Escape Symbol | Actual Symbol   | Unicode Number |
| ------------- | --------------- | -------------- |
| `\n`          | New Line        | U+000A         |
| `\t`          | Horizontal Tab  | U+0009         |
| `\r`          | Carriage Return | U+000D         |
| `\f`          | Form Feed       | U+000C         |
| `\b`          | Backspace       | U+0008         |

To be able to use `'` and `"` in single-quoted or double-quoted String Literals respectively, they can be escaped as well. This will ensure that they are treated as part of the literal, not as the terminating symbol.

```java
println "\"this is possible\" - the compiler"
println '> \' and this as well\' <'
```

The above code will print

```
"this is possible" - the compiler
> 'and this as well' <
```

To insert a backslash symbol, you can use `\\`.

```java
String path = '..\\path\\to\\file\\'
```

The value of the `path` variable will now be

```
..\path\to\file
```

## String Interpolation

By escaping an opening parenthesis symbol `\(`, one can make use of String Interpolation in Double-Quoted String Literals. The next closing parenthesis will then be treated as the continuation of the String.

```java
int value = 10
String s = "The value is: \(value)."
println s // prints 'The value is: 10.'
```

Note that this feature is only supported in Double-Quoted String Literals.

## Verbatim Strings

Verbatim Strings are a way to create Strings with many characters that would otherwise need to be escaped. This is especially handy for file paths in certain operating systems:

```java
String path = @"..\path\to\file"
```

Or for use as RegExp's, where you sometimes need to treat characters literally:

```java
String regex = @"Hello\.World" // "\." means "a literal dot symbol" in RegExp
Pattern pattern = Pattern.compile(regex)

pattern.matches("Hello.World") // => true
pattern.matches("Hello|World") // => false
```

In the example, the pattern expects a literal dot `.` rather than any character.