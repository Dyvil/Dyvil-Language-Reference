---
dyvil: v0.31.0
---

# Inheritance

Inheritance is a very common aspect of Object-Oriented Programming Languages. It allows you to define properties or behavior in a single class, and inherit them in another class without having to redefine them. This is shown in the following example:

`Person.dyvil`:

```swift
class Person
{
    let name: String
    let age: int

    func greet() -> void = print "Hello, \(name)!"
    
    // constructors omitted
}
```

`Student.dyvil`:

```java
class Student extends Person
{
    let email: String

    func send(message: String) -> void = ...
    
    // constructors omitted
}
```

The `Student` class `extends`, i.e. inherits from the `Person` class. This means that a `Student` is also a `Person`, and also has a `name` and an `age`.

```swift
let student = Student(name: "John", age: 22, email: "john@mail.com")
let person = Person(name: "Alex", age: 32)

student.greet()       // prints 'Hello, John!'    (1)
print student.age     // prints '22'              (2)
print student.email   // prints 'john@email.com'
student.send("Hi")

person.greet()        // prints 'Hello, Alex!'
print person.age      // prints '32'

print person.email    // error, because Person does not have an email field
person.send("!!!")    // error, because Person does not have a send(String) method
```

Notice how the last two statements cause a compiler error: `person` is not a `Student`, and thus does not necessarily have an `email` property. Neither do they have the `sendMail` method available for use.

The statements `(1)` and `(2)` however, are perfectly legal. The `Student` inherits the `age` property as well as the `greet` method from its parent class `Person`.

