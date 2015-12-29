# Traits and Interfaces

It is not only possible to inherit behavior from super classes. In Java, you also had the option to define `interface` and `implement` them. This powerful language feature allows the programmer to separate interface and implementation. Thus, it is also available in Dyvil, though with a minor difference.

In Dyvil, there are two kinds of contract classes, `trait`s and `interface`s. Both concepts are explained below.

## Interfaces

Interfaces mirror the pre-Java 8 `interface`s from Java. They can declare `public static final` fields and `public abstract` methods. It is not possible to instantiate an interface using the `new` operator. Interfaces are inherited from by using the `implements` keyword rather than the `extends` keyword.

```java
interface MyInterface
{
    int getMyValue() // public abstract
}

class MyClass implements MyInterface
{
    public override int getMyValue() = 10
}

MyClass myInstance = new MyClass
println myInstance.getMyValue       // prints '10'
```

In the above example, the `class MyClass` inherits the methods from the `interface MyInterface`. However, since the interface only provides the contract of the `getMyValue` method, the `MyClass` class has to provide a concrete implementation. This can be done by writing another method with the same declaration, i.e. the same name and the same parameters. To ensure that the implementation method overrides the interface method, the `override` modifier can be used. This will cause the compiler to perform additional checks and generate an error if the method doesn't override as intended.

Another important feature of interfaces is multi-inheritance.

```java
interface MyInterface2
{
    void doSomething()
}

class MyClass2 implements MyInterface, MyInterface2
{
    public override void doSomething() = println 'Hello World'
    
    public override int getMyValue() = 0
}

MyClass2 myInstance2 = new MyClass2
println myInstance2.getMyValue          // prints '0'
myInstance2.doSomething                 // prints 'Hello World'
```

## Traits

Traits are like interfaces, but with a few additional features. Like Java-8 Interfaces, Traits allow you to give methods an implementation. They are also inherited from in the `implements` list. Thus, traits allow multi-inheritance as well.

The following code snippet makes the `interface` from the Interface Example a `trait` and adds a new concrete (i.e., non-abstract) method:

```java
trait MyTrait
{
    int getMyValue() // public abstract
    
    int getMyNextValue() = this.getMyValue() + 1
}
```

Every subclass of the `MyTrait trait` now has access to the `getMyNextValue` method *without having to implement it*. This means we can use it for the `MyClass` class without having to modify it:

```java
println myInstance.getMyNextValue       // prints '11'
```