---
dyvil: v0.31.0
---

# Traits and Interfaces

It is not only possible to inherit behavior from super classes. In Java, you also had the option to define an `interface` and `implement` it. This powerful language feature allows the programmer to separate interface and implementation. In Dyvil, there are two kinds of contract classes, `trait`s and `interface`s. Both concepts are explained below.

## Interfaces

Interfaces in Dyvil mirror the `interface`s from before Java 8. They can declare `const` fields and `abstract` methods. It is not possible to instantiate an interface using the `new` operator. Interfaces are inherited from by using the `implements` keyword rather than the `extends` keyword.

```swift
interface MyInterface
{
    /* public abstract */ func getMyValue() -> int
}

class MyClass implements MyInterface
{
    override func getMyValue() -> int = 10
}

let myInstance = new MyClass
print myInstance.getMyValue  // prints '10'
```

In the above example, the class `MyClass` inherits the methods from the interface `MyInterface`. However, since the interface only provides the signature of the `getMyValue` method, the `MyClass` class has to provide a concrete implementation. This can be done by writing another method with the same declaration, i.e. the same name and the same parameters. To ensure that the implementation method overrides the interface method, the `override` modifier can be used. This will cause the compiler to perform additional checks and display a diagnostic error message if the method doesn't override as intended.

An import difference between classes and interfaces is the fact that the latter supports multiple inheritance. This means a class or interface can implement more than one interface.

```swift
interface MyInterface2
{
    func doSomething() -> void
}

class MyClass2 implements MyInterface, MyInterface2
{
    // from MyInterface2
    override func doSomething() -> void = print 'Hello World'

    // from MyInterface
    override func getMyValue() -> int = 0
}

let myInstance2 = new MyClass2
print myInstance2.getMyValue // prints '0'
myInstance2.doSomething      // prints 'Hello World'
```

## Traits

Traits are like interfaces, but with a few additional features. Like Java-8 Interfaces, Traits allow you to give methods an implementation. Like interfaces, they are inherited from using the `implements` keyword and allow multi-inheritance.

The following code snippet makes the `interface` from the Interface Example a `trait` and adds a new concrete \(i.e., non-`abstract`\) method:

```java
trait MyTrait
{
    func getMyValue() -> int

    func getMyNextValue() -> int = this.getMyValue() + 1
}
```

Every subclass of the `MyTrait trait` now has access to the `getMyNextValue` method _without having to implement it_. This means we can use it for the `MyClass` class without having to modify it:

```java
println myInstance.getMyNextValue       // prints '11'
```



