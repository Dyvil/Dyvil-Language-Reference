---
dyvil: v0.32.0
---

# Constructors

Constructors are a way to create instances of objects. They are declared like a method, with the difference being the `new` keyword instead of a method name. The following class in Java:

```java
class MyClass
{
    public MyClass()
    {
        // ...
    }
}
```

Looks like this in Dyvil:

```java
class MyClass
{
    public new()
    {
        // ...
    }
}
```

This allows you to construct an instance of the `MyClass` class:

```swift
let myInstance = new MyClass
print myInstance // prints 'MyClass@abcdef'
```

---

Constructors may also define parameters, just like methods:

```java
class MyIntContainer
{
    var value: int
    
    public new(value: int)
    {
        this.value = value
    }
    
    func getValue() -> int = this.value
}
```

As with methods, you have to pass arguments for these parameters when invoking the constructor:

```swift
let container = new MyIntContainer(10)
print container.getValue // prints '10'
```

As shown above, empty parenthesis may be omitted from constructor calls.

---

Dyvil also provides a way to use constructors with generics. The following example shows just that:

```java
class MyContainer<T>
{
    var value: T
    
    public new(value: T)
    {
        this.value = value
    }
    
    func getValue() -> T = this.value
}
```

```swift
let container = new MyContainer<String>("abc")
    // inferred type MyContainer<String>
println container.getValue                      // prints 'abc'
```

In the above example, you don't have to explicitly declare the type argument. The compiler can also infer it from the type of the argument `"abc"` (which is `String`).

```swift
let container = new MyContainer("abc")
    // inferred type MyContainer<String>
let value = container.getValue
    // inferred type String
```