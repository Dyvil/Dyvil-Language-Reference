---
dyvil: v0.32.0
---

# Initializer Blocks

**Initializer Blocks** are a way to run code during the initialization of a class or an instance. You can declare one by using the `init` keyword in a class body:

```java
class Foo
{
    var bar: int
    
    init
    {
        var i: int = someValue
        if (someCondition)
        {
            i *= 2
        }
        this.bar = i
        
        print "Initialized"
    }
}

new Foo // prints 'Initialized'
```

When creating an instance of the `Foo` class, the initializer block runs as if it was part of a constructor body. There is a major difference between initializer blocks and no-arg constructors, however. While the latter are separate and only one of them runs, initializers are shared. This means they run regardless of which constructor was called.

```java
class Bar
{
    public new(i: int)
    {
        print "new(int)"
    }
    
    public new(s: String)
    {
        print "new(String)"
    }
    
    init
    {
        print "Initializer"
    }
}

new Bar(1)   // prints 'Initializer', 'new(int)'
new Bar("A") // prints 'Initializer', 'new(String)'
```

## Static Initializer Blocks

Adding the `static` modifier makes a **Static** or **Class** initializer. They run at most once, when the enclosing class is loaded.

```java
class Baz
{
    static init
    {
        print "Static Init"
    }
    
    init
    {
        print "Init"
    }
}

new Baz // prints 'Static Init', 'Init'
new Baz // prints 'Init'
new Baz // prints 'Init'
```