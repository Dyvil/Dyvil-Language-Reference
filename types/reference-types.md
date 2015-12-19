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

Using the `*` operator, you can create reference to the following kinds of data members:

- Local Variables
- Instance Fields
- Static Fields
- Class Parameters

It is not possible to reference a method parameter or a property (instance or static). Doing so will result in a compiler error.

## Reference Parameters

When writing the signature for an ordinary method, parameters can have the `var` modifier. This allows you to pass one of the above data members, which will be converted to an implicit reference. It is not required to use the `*` operator at the use site:

```java
static void inc(var int i, int n) = i += n

int myInt = 0
inc myInt
println myInt // prints 1
inc(myInt, 10)
println myInt // prints 11

inc(*myInt) // disallowed
```
