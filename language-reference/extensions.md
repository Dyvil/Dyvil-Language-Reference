# Extensions

Extensions are a powerful language feature that is inspired by Swift. Extensions allow you to modify an existing class without editing its source, for example to add new functionality to Strings or Arrays. You can do any of the following:

* Add new methods
* Add new computed properties
* Add new fields

Extensions are unnamed and can be used via [headers](../headers.md). Here is a simple example:

```swift
extension String {
    static func empty() -> String = ""

    func size() -> int = this.length()
}
```

This extension applies to the class `String` and all instances. You can use it like this:

```swift
String.empty() // => ""
"abc".size() // => 3
```

### Extension Functions

Extensions are actually just syntactic sugar for extension methods. They can be added in any class, making them useful when combined with regular utility methods.

```swift
class Arrays {
    final extension func in<T>(this: T, array: [T]) = array.contains(this)
}
```

This is especially useful if you want to use the extension methods as static utilities from Java code. Now the extension class has a name (Arrays) that can easily be used.

```java
import org.example.Arrays

Arrays.in("a", new String[] { "a", "b", "c" }) // => true
```

### Generic Extensions

Extensions may also be generic, which is useful for extending generic types or arrays:

```swift
extension<T> List<T> {
    func first() -> T = this.get(0)
}

extension<T> [T] {
    func first() -> T = this[0]
}
```

With that in mind, we can also show how extensions with computed properties can be useful:

```swift
extension<T> [T] {
    var first: T {
        get { return this[0] }
        set { this[0] = newValue }
    }
}

let arr = [1, 2, 3]
arr.first // => 1
arr.first = 0
arr[0] // => 0
```

### Extension Methods and Overrides

Extension methods interact with inheritance and method overrides. Consider this class structure:

```swift
class A {}
class B extends A {
    func foo() -> String = "B"
}

extension A {
    func foo() -> String = "A"
}
```

Now there are two different scenarios: `A.foo` is called on an instance of `A`, or on an instance of `B`:

```swift
let a = new A()
let b = new B()
let bA: A = b

a.foo() // => "A" (via extension)
b.foo() // => "B" (via B's implementation through regular method invocation)
bA.foo() // => "B" (via B's implementation through dynamic method invocation)
```

{% hint style="warning" %}
Internally, extension methods use a dynamic invocation instruction called `INVOKEDYNAMIC` along with some special code that looks for overridden methods at runtime. This may have a performance impact.
{% endhint %}

You can prevent dynamic dispatch of extension methods by making the method final. Static extensions methods never dispatch dynamically.

{% hint style="info" %}
Extending a final class like String does not prevent dynamic dispatch. The extended class might add the extension methods in the future, and invocations should switch to the regular implementation without recompiling.
{% endhint %}
