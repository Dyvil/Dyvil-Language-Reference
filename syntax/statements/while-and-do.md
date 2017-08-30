# While Statements

While Statements are the most basic form of loop in Dyvil. They consist of a head and a body.

```swift
while condition { statements... }
while (condition) expression
```

A While Statement always checks the condition first. If it evaluates to `true`, the body is executed. Afterwards, the condition is checked again and if it is still `true`, the body is executed again. This process is repeated until the condition evaluates to `false`, or the body is left using `break` or `return` statements or exceptions. A While Statement can not return a value itself and always has the type `void`.

The following example illustrates how a While Statement can be used to display numbers.

```swift
var i = 1
while i <= 5
{
    i++
}

// prints 1, 2, 3, 4, 5
```

