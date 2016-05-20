# Parameters

**Parameter** can be used in two different ways: As method parameters and as class parameters.

## Method Parameters

Method Parameters are used in every method and constructor declaration:

```java
int add(int l, int r) = r + l
            ^      ^
```

In the above example, `l` and `r` are parameters of the `add` method. Both parameters are of type `int`. When calling the `add` method, you will have to pass two arguments that are either `int`s or can be implicitly converted to `int`.

```java
int i1 = add(1, 2) // 3
int i2 = add(2, i1) // 5
int i3 = add(i1, i2) // 8

short s = -1
byte b = 2
// s and b can be converted to int
int i4 = add(s, b) // 1
```

## Class Parameters

Class Parameters are similar Method Parameters, but declared on classes.

```java
class IntAndString(int i, String s)
```

By annotating a class with parameters, you can force the compiler to generate fields and a constructor. The above Dyvil class definition would look like this in Java:

```java
class IntAndString
{
    int i;
    String s;
    
    public IntAndString(int i, String s)
    {
        this.i = i;
        this.s = s;
    }
}
```

As you can see, using class parameters saves you a lot of boilerplate code. Still, an instance of the `IntAndString` class has to created like this:

```java
IntAndString ias = new IntAndString(1, "a")
```

Class Parameters are even more useful in [Case Classes](classes/case-classes.md).
