---
dyvil: v0.34.0
---
# Tuples

**Tuples** are special data structures that allow you to store multiple values in one object without having to declare an extra class. Unlike arrays, tuples values can be of different type, and tuples of different lenghts are incompatible with each other.

```swift
(value1, value2, ...)
```

The type of a tuple is always `(type of value1, type of value2, ...)`, which is a tuple type with the same arity as the tuple expression. As with arrays, providing an explicit type for tuple expressions via casts or type ascriptions makes the expression convert its subexpressions. The following example code illustrates the type behaviour of tuples.

```swift
let t = (1, "a", true) // t: (int, String, boolean)
let u = (1, 2) // t: (int, int)

let v: (int, float) = (1, 2)
```

The most important tuple operations are the `_n` accessors, where `n` can be any number from `1` to the arity the tuple.

```swift
print t._1 // prints 1

let s = t._2 // s: String
print s // prints a
print t._3 // prints true
```

More tuple operations can be found in the `dyvil.tuple.Tuple` class and its nested classes.