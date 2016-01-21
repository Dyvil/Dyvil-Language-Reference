# Methods

**Methods** are one of the most important aspects in all programming languages. They roughly represent **functions** in mathematics. They take zero or more [parameters](classes/parameters.md) and compute and return an output value.

In Dyvil, methods can be declared within classes. In the following example, the `Dog` class has a method named `say` that prints something to the console. It takes no parameters and doesn't return a result (as indicated by the return type `void`).

```java
class Dog(String name)
{
    public void say()
    {
        println "Woof"
    }
    
    public String getName() = this.name
    
    public void setName(String newName)
    {
        this.name = newName
    }
}
```

The `String getName()` is also a method, as indicated by the (empty) parameter list in parenthesis `()`. It doesn't take any parameters either, but returns a result of type `String`, namely the name of the dog. This is usually referred to as a **Getter Method**. The `getName` method uses an inline expression using the `=` symbol. It could also be written in brace-style:

```java
public String getName()
{
    return this.name
}
```

There is no semantic difference between the two versions, though the second one is more verbose.

`setName` is a so-called **Setter Method**. It takes a single parameter of type `String` called `newName` and doesn't return a result (see `void`). The implementation replaces the old name of the dog with the `newName` (i.e. renames the dog). It uses brace-style notation, but could also be written inline:

```java
public void setName(String newName) = this.name = newName
```

Due to the two `=` symbols, this style is not advised.

## Method Parameters

Methods can take an arbitrary amount of [**Parameter**s](classes/parameters.md). They are usable in the method implementation and have to be passed at the call site (when calling the method). Method parameters are always declared within parenthesis after the method name. Multiple parameters are separated with a comma `,`.

```java
public void foo() = println "Hello World"           // zero parameters
public int  negate(int i) = -i                      // one parameters
public int  add(int i, int j) = i + j               // two parameters
public int  add3(int i, int j, int k) = i + j + k   // three parameters

// ...
```

Methods without parameters require the `()` notation. Otherwise, they will be considered a [field](classes/fields.md) or [property](classes/properties.md) by the parser.

```java
public String getName = this.name   // field
public String Name { ... }          // property
public String getName() = this.name // method
public String Name() { ... }        // method
```