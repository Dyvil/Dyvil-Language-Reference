---
dyvil: v0.31.0
---

# Classes

Dyvil is an object-oriented programming language. And like every other OOP language, it has some notion of Classes. They allow you to group common behavior and properties into one structure that describes objects. The example below displays how a common example, the `Person` class, can be written in Dyvil:

```swift
class Person
{
    let name: String
    let age: int

    func greet() -> void = print "Hello, \(name)!"
    
    // constructors omitted
}
```

The `Person` class has two properties, a `name` and an `age`. The `name` is a String of characters that holds the name of the person. The `age` describes how old the person is, in years.

You will also notice the `greet` method. Given some `person`, you can call it like

```swift
let person = Person("Peter", 20)
person.greet() // prints "Hello, Peter"
```

---

The following chapters will guide you through all the language features related to classes and class members.

