# Import, Using and Include Declarations

## Import Declarations

An import declaration can be used as follows

```scala
import dyvil.collection.mutable.ArrayList
```

This makes the type `ArrayList` in the `dyvil.collection.mutable` package available in the current scope. Furthermore, it is also possible to import multiple types at once, as shown below:

```scala
import dyvil.collection.immutable.{ ArraySet, EmptyList }
```

This allows you to import both the `ArraySet` and `EmptyList` types without having to re-type the package. Alternatively, it is also possible to import *all* types in a given package, using the `_` keyword:

```scala
import dyvil.collection.range._ // imports all types in the 'dyvil.collection.range' package
```

## Using Declarations

Using Declarations share the same syntax with Import Declarations, but function differently. They import members such as methods or fields, while `import` operates on classes and packages.

As an example, a Using Declaration allows you to import all methods of the utility class `dyvil.string.StringUtils` into the current scope:

```scala
using dyvil.string.StringUtils._
```

This makes it possible to use `infix` methods from the class without having to manually type out the class name:

```java
// old way:
import dyvil.string.StringUtils
String s = StringUtils.toIdentifier("Hello World")

// new way:
using dyvil.string.StringUtils._
String s = "Hello World".toIdentifier
```

Using Declarations are the Dyvil equivalent of `import static` in Java, but also allow multi-imports using `{ }`, as shown above.

## Include Declarations

Using Include Declarations, you can import all Header Declarations from a Header File.
For example, the include declaration

```java
include dyvil.Collections
```

Will ensure that all Imports and Operators defined in the `dyvil.Collections` header are available in the current scope. This also works for imported members and types within the included header. An example for this would be

```java
include dyvil.Arrays
```

This adds all array utility classes in the `dyvil.array` package to the current scope.

Include Declarations can also be present within Headers themselves. This allows deeply nested structures of Headers to be included with a single statement.

**Example**:

`HeaderA.dyh`:
```
import com.example.ClassA
```

`HeaderB.dyh`:
```
import com.example.ClassB
include HeaderA
```

`MyClass.dyh`:
```
class MyClass
{
    ClassA classA = ... // available in current scope
    ClassB classB = ... // ditto
}
```
