---
dyvil: v0.31.0
---

# Comments

Dyvil inherits the comment style from Java. There are three types of comments, all of which are completely ignored by the compiler and REPL. DyvilDoc comments are processed by Documentation tools.

## Single-Line Comments

Single line comments span a single line, or the last part of it. They are started with two slashes `//` and terminated by a newline.

```java
// this is a comment
print "Hello World"  // this is another comment
```

## Multi-Line Comments

Multi-line comments span multiple lines. You can indicate a multi-line comment using a slash and an asterisk `/*` and end them with the same characters in reverse order `*/`.

```java
/* this is a multi-
   line comment */
print "This is code"
print /* You can put comments in between code as well */ "And this as well"
```

## DyvilDoc Comments

As in Java, Dyvil also supports comments for Documentation. They are written in the DyvilDoc format and span multiple lines. They are indicated with a slash and two asterisks `/**` and terminated like normal multi-line comments \(`*/`\).

```swift
class Player
{
    /**
     * Stores the name of the player
     */
    var name: String
}
```

