# Fields

Fields are a way to store information about objects of a class. They are declarated using the `var` and `let` keywords:

```swift
class Person
{
    let id: long = randomID()
    var name: String
    var age: int
}
```

You can declare fields with or without an initial value. If no initial value is declared, it will be the default value for the type of the field. See the table in [Wildcard Literals](/syntax/other-literals.md "Wildcard Literals") for more information.

## Initialization

Instance fields, i.e. non-`static` fields are initialized as soon as an object of the class is constructed.

```swift
class Test
{
    var s: String = { print "Init"; "." }
}

new Test // prints 'Init'
new Test // prints 'Init'
```

Static fields belong to the class itself, not individual members. This means they are initialized only once: when the class gets reference for the first time.

```swift
class Test
{
    static var s: String = { print "Init"; "." }
}

new Test // prints 'Init'
new Test // does not print 'Init' again
```

## Final Fields and `let` Declarations

The `final` modifier or `let` declarator makes a field immutable. This means it cannot be re-assigned after it has been set to an initial value. Attempting to re-assign a final field will result in a compilation error.

```java
class Test
{
    let i: int = 1
    final var j: int = 2
}

let t = new Test
t.i = 3 // invalid, cannot reassign final field 'i'
t.j = 3 // invalid, s.a.
```

All final fields have to be initialized with an initial value, or a compilation error will be issued.



