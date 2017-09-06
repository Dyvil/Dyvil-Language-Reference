---
dyvil: v0.34.0
---
# If Statements

If Statements are a language construct that can be used to change the behaviour of the program depending on a condition.
They consist of a head, a body and an optional else branch.

```swift
// without else
if condition expression
if condition { statements... }

// with else:
if condition expression else expression
if condition { statements... } else { statements... }

// parentheses around the condition are optional
```

The semantics of an If Statements are as follows:

1. Evaluate the condition
2. If the result has a boolean value of `true`, evaluate the 'then' branch and return the result
3. Otherwise, evaluate the 'else' branch if it exists and return the result.

The following program illustrates this behaviour:

```swift
let condition = 1 < 2
if condition
{
    print("1 < 2")
}
else
{
    print("something went wrong")
}

// prints "1 < 2"
```

If Statements may also be used in contexts where an expression is expected, e.g. as a method argument:

```swift
let condition = true
print(if (condition) 1 else 2)

// prints 1
```

Note that in simple cases like the above, a Ternary Conditional Operator should be used instead of an If Expression.

```swift
print(condition ? 1 : 2)
```

Using an If Expression without an Else branch in an expression context causes an error diagnostic.

## Binding If Statements

Binding If Statements are a special form of If Statements meant for use with Optional Values. Instead of a condition, their head consists of a variable binding that can have an arbitrary type:

```swift
if let name = expression { statements... }
// with else and explicit type
if let name: Type = expression { statements... } else { statements... }
```

The semantics of a Binding If Statement differ from those of a normal If Statement:

1. Evaluate the expression after the `=` of the variable.
2. If the result is not `null`, bind it to the variable name and evaluate the 'then' branch. The variable name is available in the scope of the 'then' branch.
3. If the result was `null`, evaluate the 'else' branch. The variable name is not available in this scope.

The example below uses a Binding If Statement to check if certain data is available.

```swift
case class Person(firstName: String, middleName: String?, lastName: String)
let person = Person("John", null, "Doe")

if let middleName = person.middleName
{
    print("\(person.firstName) \(middleName) \(person.lastName)")
}
else
{
    print("\(person.firstName) \(person.lastName)")
}
```

The program prints "John Doe" when executed. Changing the second line to `let person = Person("John", "Peter", "Doe")` causes it to print "John Peter Doe" instead.

As with If Statements, Binding If Statements may also be used in expression contexts.