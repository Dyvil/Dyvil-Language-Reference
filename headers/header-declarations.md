# Header Declarations

Headers and Class Files can be optionally attributed with a Header Declaration. This allows you to use Class Files in `using` declarations and makes it possible to give a header custom access modifiers and annotations:


`MyClass.dyv`:

```java
import java.util.{ Map, HashMap }

public @Annotated header MyClass

public class MyClass
{
    ...
}
```

`MyOtherClass.dyv`:

```java
using MyClass

public class MyOtherClass
{
    static func main(args: [String]) -> void
    {
        let map: Map<String, String> = new HashMap<String, String> // no explicit import required
    }
}
```