# Initializer Blocks

**Initializer Blocks** are a way to run code during the initialization of a class or an instance. You can declare one by using the `init` keyword in a class body:

```java
class Foo
{
    final int bar
    
    init
    {
        int i = someComputation()
        if (someCondition)
        {
            i *= 2
        }
        this.bar = i
        
        println "Initialized"
    }
}

new Foo // prints 'Initialized'
```

When creating an instance of the `Foo` class, the initializer block runs as if it was part of a constructor body. There is a major difference between initializer blocks and no-arg constructors, however. While the latter are separate and only one of them runs, initializers are shared. This means they run regardless of which constructor was called.

```java
class Bar
{
    public new(int i)
    {
        println "new(int)"
    }
    
    public new(String s)
    {
        println "new(String)"
    }
    
    init
    {
        println "Initializer"
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
        println "Static Init"
    }
    
    init
    {
        println "Init"
    }
}

new Baz // prints 'Static Init', 'Init'
new Baz // prints 'Init'
new Baz // prints 'Init'
```