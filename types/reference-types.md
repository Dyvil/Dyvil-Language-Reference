---
dyvil: v0.31.0
---

# Reference Types

In Dyvil, you have the option to create objects that represent pointers to fields. You can accomplish this by using reference types, which are declared using the postfix type operator `*`:

```swift
var myInt:    int  = 0
var myIntRef: int* = &myInt

var string:    String  = "abc"
var stringRef: String* = &string
```

As shown, a reference to a field can be created with the prefix `&` operator. Once you have the reference, you can use the `*` and `* =` operators to change the value of the underlying field:

```swift
print *intRef      // prints 0
print *stringRef   // prints 'abc'

*myIntRef = 10
print *myInt       // prints 10
print *myIntRef    // prints 10
```

Any changes made to the field will be instantly applied to the pointer object, and vice-versa.

```swift
string = "def"
print *stringRef   // prints 'def'

*stringRef = "test"
print *string           // prints 'test'
```

## The `&` Operator

The `&` prefix operator \(read 'Reference Operator'\) allows you to reference a data member. The following data members are allowed as the operand, as long as they are non-`final`:

* Local Variables
* Instance Fields
* Static Fields
* Class Parameters
* Properties \(pairs of getter and setter methods\)
* Array Elements:

```swift
let myArray: [int] = [ 1, 2, 3 ]
let myArrayRef: int* = &myArray[0]

print *myArrayRef    // prints '1'
*myArrayRef = 10
print myArray        // prints '[10, 2, 3]'
```

## Implicit Reference Types

Implicit Reference Types are denoted with the postfix type operator `^` instead of `*`. This will make it possible to directly pass an expression without having to use the reference operator `&`. Furthermore, Implicit Reference Types can be implicitly de-referenced.

```swift
func inc(i: int^, n: int) -> void
{
    let newValue = i + 1 // no de-referencing required
    *i = newValue        // assign the new value to the reference target
    
    i = newValue // this does NOT assign the new value to the original variable
                 // instead, it tries to store a reference to the 'newValue' variable to i
                 // this causes a compiler error because newValue is final
}

var myInt: int = 0
var myRef: int^ = myInt // no explicit '&' required

inc myInt
print myInt // prints 1

inc(myRef, 10)
print myInt // prints 11
```



