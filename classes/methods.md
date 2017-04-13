---
dyvil: v0.31.0
---

# Methods

**Methods** are one of the most important aspects in all programming languages. They roughly represent **functions** in mathematics. A method can take zero or more [parameters](/classes/parameters.md) and compute and return an output value or perform side effects.

In Dyvil, methods can be declared within classes. In the following example, the `Dog` class has a method named `say` that prints something to the console. It takes no parameters and doesn't return a result \(as indicated by the return type `void`\).

```swift
class Dog
{
    var name: String

    func say() -> void = print "Woof"

    func getName() -> String = this.name

    func setName(newName: String) -> void
    {
        this.name = newName
    }
}
```

`getName` is also a method, as indicated by the \(empty\) parameter list in parenthesis `()`. It doesn't take any parameters either, but returns a result of type `String`, namely the name of the dog. This is usually referred to as a **Getter Method**. The `getName` method uses an inline expression using the `=` symbol. It could also be written in brace-style:

```swift
func getName() -> String
{
    return this.name
}
```

There is no semantic difference between the two versions, though the second one is more verbose.

`setName` is a so-called **Setter Method**. It takes a single parameter of type `String` called `newName` and doesn't return a result \(see `void`\). The implementation replaces the old name of the dog with the `newName` \(i.e. renames the dog\). It uses brace-style notation, but could also be written inline:

```swift
func setName(newName: String) -> void = this.name = newName
```

## Method Parameters

Methods can take an arbitrary amount of [Parameters](/classes/parameters.md). They are usable in the method implementation and have to be passed at the call site \(when calling the method\). Method parameters are always declared within parenthesis after the method name. Multiple parameters are separated with a comma `,`.

```swift
func foo() = print "Hello World"                // zero parameters
func negate(i: int) -> int = -i                 // one parameters
func add(i: int, j: int) -> int = i + j         // two parameters
func add3(i: int, j: int, k: int) = i + j + k   // three parameters
```



