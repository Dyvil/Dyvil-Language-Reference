# Fields

Fields are a way to store information about objects of a certain class. They are created with the same notation as in Java:

```java
class Person
{
    String name
    int age = 20
]
```

You can declare fields with or without an initial value. If no initial value is declared, it will be the default value for the type of the field.

| Type            | Initial Value |
|-----------------|---------------|
| `boolean`       | `false`       |
| integer         | `0`           |
| floating point  | `0.0`         |
| reference types | `null`        |

## Initialization

When declaring a field with an initial value, that value has to be assigned to the field at some point in time. This point depends on if the field is `static` or not, and if it is initialized `lazy`ly or not.

Normal fields, i.e. non-`static` non-`lazy` fields are initialized as soon as an object of the class is constructed.

```java
public class Test
{
    String s = { println "Init"; "." }
}

new Test // prints 'Init'
new Test // prints 'Init'
```

Static fields belong to the class itself, not individual members. This means they are initialized only once: when the class gets loaded.

```java
public class Test
{
    static String s = { println "Init"; "." }
}

new Test // prints 'Init'
new Test // does nothing
```

Lazy fields are initialized not when an object or class is loaded, but when the field is used for the first time:

```java
public class Test
{
    lazy String s = { println "Init"; "." }
}

Test t = new Test // does nothing
t.s // prints 'Init'
t.s // does nothing
new Test.s // prints 'Init'
```

Static lazy fields behave like their modifiers suggest. They are only initialized once, when they are used.

```java
public class Test
{
    static lazy String s = { println "Init"; "." }
}

Test.s // prints 'Init'
Test.s // does nothing
```

## Final Fields

The `final` modifier makes a field immutable. This means it cannot be re-assigned after it has been set to an initial value, otherwise the compiler will cause an error.
  
```java
final String name

public void setName(String newName)
{
    this.name = newName // illegal
}
```

All final fields have to be initialized either with an initial value or in all constructors individually. Otherwise, the compiler will tell you about the mistake via an error.