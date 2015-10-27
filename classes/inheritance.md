# Inheritance

Inheritance is a very common aspect of Object-Oriented Programming Languages. It allows you to define properties or behavior in a single class, and inherit them in another class without having to redefine them. This is shown in the following example:

`Person.dyvil`:
```java
class Person
{
    String name
    int age
    
    public void sayHello() = println "Hello, \(name)!"
}
```

`Student.dyvil`:
```java
class Student extends Person
{
    String email
    
    public String sendEmail(String text) = ...
}
```

The `Student` class `extends`, i.e. inherits from the `Person` class. This means that a `Student` is also a `Person`, and also has a `name` and an `age`.

```java
Student student = Student(name: "John", age: 22, email: "john@mail.com")
Person person = Person(name: "Alex", age: 32)

student.sayHello()      // prints 'Hello, John!'    (1)
println student.age     // prints '22'              (2)
println student.email   // prints 'john@email.com'
student.sendMail("Hi")

person.sayHello()       // prints 'Hello, Alex!'
println person.age      // prints '32'
println person.email    // error
person.sendMail("!!!")  // error
```

Notice how the last two statements cause a compiler error: `person` is not a `Student`, and thus does not necessarily have an `email` property. Neither do they have the `sendMail` method available for use.

The statements `(1)`, `(2)` and `(3)` however, are perfectly legal. The `Student` inherits the `age` property as well as the `sayHello` method from its parent class, `Person`.