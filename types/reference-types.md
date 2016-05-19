# Reference Types

In Dyvil, you have the option to create objects that represent pointer to fields. You can accomplish this by using reference types, suffixed with a `*` sign:

```java
int myInt = 0
int* intReference = &myInt

String string = "abc"
String* stringReference = *string
```

As shown, a reference to a field can be created with the prefix `&` operator.

Once you have the reference, you can either `get` or `set` it:

```java
println intReference.get      // prints 0
println stringReference.get   // prints 'abc'

intReference.set 10
println myInt                 // prints 10
println intReference.get      // prints 10
```

Any changes made to the field will be instantly applied to the pointer object, and vice-versa.

```java
string = "def"
println stringReference.get   // prints 'def'
stringReference.set "test"
println string                // prints 'test'
```

## The `&` Operator

The `&` prefix operator (read 'Reference Operator') allows you to reference a data member. The following data members are allowed as the operand:

- Local Variables
- Instance Fields
- Static Fields
- Class Parameters
- Properties (pairs of getter and setter methods)

Array elements (array + index) can also be referenced:

```java
[int] myArray = [ 1, 2, 3 ]
int& myArrayReference = &myArray[0]

println myArrayReference.get    // prints '1'
myArrayReference.set 10
println myArray         // prints '[10, 2, 3]'
```

The expression on which the subscript is used does not need to be a direct field access. It is also possible (though not recommended) to use more complex expressions here:

```java
[int] getArray() = ...

int* myArrayReference = &getArray()[]    // method call

int* myArrayPointer = &(new [int](3))[0] // array constructor

int* myArrayPointer = &{                 // code block
    [int] ints = [];
    ints += 1;
    ints
}[0]
```

## Implicit Reference Types

Implicit Reference Types are denoted with a `^` instead of `*`. This will make it possible to directly pass an expression without having to use the reference operator `&`. Furthermore, Implicit Reference Types can be implicitly de-referenced.

```java
static void inc(int^ i, int n)
{
    let newValue = i + 1 // no de-referencing required
    *i = newValue        // assign the new value to the reference target
}

int myInt = 0
int^ myRef = myInt // no explicit '&' required

inc myInt
println myInt // prints 1

inc(myRef, 10)
println myInt // prints 11
```
