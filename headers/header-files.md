---
dyvil: v0.31.0
---

# Header Files

**Header Files** are a special file type that allows the collection of Import and Using Declarations, Operators and Type aliases. They are created with the `.dyh` or `.dyvilh` file extension and allow the definition of the above header elements, but not classes.  
To use header files from within other files, one can include them with the `using` keyword. This has the same effect as copying the code from the header into the source file:

`MyHeader.dyh`:

```java
import java.util.List
import java.util.ArrayList
```

`MyClass.dyv`:

```java
using MyHeader

class MyClass
{
    static func main(args: [String]) -> void
    {
        let list: List<String> = new ArrayList<String> // no explicit import required
    }
}
```

Header Files differ from other class files in that they are not compiled to `.class` files, but to an object code representation with the `.dyo` file extension.  
The file type stores all import and using declarations, operator definitions and type aliases in a binary format. This ensures that the entire source code of the Header File \(excluding comments\) can be rebuilt from the object code.

