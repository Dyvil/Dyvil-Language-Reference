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

```java
MyClass myInstance = new MyClass
println myInstance                  // prints 'MyClass@abcdef'
```

---

Constructors may also define parameters, just like methods:

```java
class MyIntContainer
{
    private final int value;
    
    public new(int value)
    {
        this.value = value;
    }
    
    public int getValue() = this.value
}
```

As with methods, you have to pass arguments for these parameters when invoking the constructor:

```java
MyIntContainer container = new MyIntContainer(10)
println container.getValue          // prints '10'
```

As shown above, empty parenthesis may be omitted from constructor calls.

---

Dyvil also provides a way to use constructors with generics. The following example shows just that:

```java
class MyContainer[T]
{
    private final T value;
    
    public new(T value)
    {
        this.value = value;
    }
    
    public T getValue() = this.value
}
```

```java
auto container = new MyContainer[String]("abc")
    // inferred type MyContainer[String]
println container.getValue                      // prints 'abc'
```

In the above example, you don't have to explicitly declare the type argument. The compiler can also infer it from the type of the argument `"abc"` (which is `String`).

```java
auto container = new MyContainer("abc")
    // inferred type MyContainer[String]
auto value = container.getValue
    // inferred type String
```