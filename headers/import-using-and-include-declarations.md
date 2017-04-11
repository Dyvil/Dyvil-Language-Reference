---
dyvil: v0.31.0
---

# Import Declarations

An `import` declaration can be placed in a header file or the header of a class file. It uses the following syntax:

```scala
import dyvil.collection.mutable.ArrayList
```

This makes the type `ArrayList` in the `dyvil.collection.mutable` package available in the current scope. Furthermore, it is also possible to import multiple types at once, as shown below:

```scala
import dyvil.collection.immutable.{ ArraySet, EmptyList }
```

This allows you to import both the `ArraySet` and `EmptyList` types without having to re-type the package. To import _all_ types in a given package, you can use the special `_` symbol, called a Wildcard Import this this context:

```scala
import dyvil.collection.range._ // imports all types in the 'dyvil.collection.range' package
```

Import Declarations can not only be used to import classes. By placing one ore more of the following keywords after `import`, you can opt in for different member kinds.

| Keyword | Member Kind |
| :--- | :--- |
| `package` | Packages |
| `header` | Headers |
| `type` | Type Aliases and Type Members |
| `class` | Classes, Interfaces and Traits |
| `func` | Static Methods |
| `var` or `const` | Static Fields |
| `static` | Static Fields or Methods |
| `implicit` | Implicit Static Methods |
| `inline` \(implies `header`\) | All header declarations from the header |

Without any keyword, all member kinds will be imported. The `using` keyword is equivalent to `import static inline` , i.e. it imports static methods and header declarations.

### Examples

```swift
// Package Imports
import package dyvil.collection.mutable
let list: mutable.ArrayList = new mutable.ArrayList()

// Type Imports
import type dyvil.lang.Lang.Configure
func f(c: Configure<String>) = c("abc")

// Function Imports
import func java.lang.String.valueOf
let s: valueOf(10)

// Field Imports
import const java.lang.Integer.MAX_VALUE
let i = MAX_VALUE

// Implicit Imports
import implicit dyvil.lang.Strings.s2Name
let n: Name = "abc"

// Inline Imports
import inline dyvil.lang.Lang // this import declaration is implicitly present in every Dyvil file
```

