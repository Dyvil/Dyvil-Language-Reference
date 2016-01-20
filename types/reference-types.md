# Reference Types

In Dyvil, you have the option to create objects that represent pointer to fields. You can accomplish this by using reference types, suffixed with a `*` sign:

```java
int myInt = 0
int* intPointer = *myInt

String string = "abc"
String* stringPointer = *string
```

As shown, a reference to a field can be created with the prefix `*` operator.

Once you have the reference, you can either `get` or `set` it:

```java
println intPointer.get      // prints 0
println stringPointer.get   // prints 'abc'

intPointer.set 10
println myInt               // prints 10
println intPointer.get      // prints 10
```

Any changes made to the field will be instantly applied to the pointer object, and vice-versa.

```java
string = "def"
println stringPointer.get   // prints 'def'
stringPointer.set "test"
println string              // prints 'test'
```

## The `*` Operator

The `*` prefix operator (read 'Reference Operator') allows you to reference a data member. The following data members are allowed in this process:

- Local Variables
- Instance Fields
- Static Fields
- Class Parameters

It is not possible to reference a method parameter or a property (instance or static). Doing so will result in a compiler error.

Array elements (array + index) can also be referenced:

```java
[int] myArray = [ 1, 2, 3 ]
int* myArray0 = *myArray[0]

println myArray0.get    // prints '1'
myArray0.set 10
println myArray         // prints '[10, 2, 3]'
```

The expression on which the subscript is used does not need to be a direct field access. It is also possible (though not recommended) to use more complex expressions here:

```java
[int] getArray() = ...

int* myArrayPointer = *getArray()[]

int* myArrayPointer = *(new [int](3))[0]

int* myArrayPointer = *{
    [int] ints = [];
    ints += 1;
    ints
}[0]
```

## Reference Parameters

When writing the signature for an ordinary method, parameters can have the `var` modifier. This allows you to pass one of the above data members, which will be converted to an implicit reference. It is not required (and disallowed) to use the `*` operator at the use site:

```java
static void inc(var int i, int n) = i += n

int myInt = 0

inc myInt
println myInt // prints 1

inc(myInt, 10)
println myInt // prints 11

inc(*myInt) // disallowed
```
