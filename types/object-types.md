# Object Types

Reference types are named references to existing non-generic types. They are, among generic types, the most commonly used types in Dyvil. As of Dyvil 1.0, it is not possible to qualify type names. Instead, the qualified package name has to be `import`ed before the type can be used, unless the type is implicitly imported through the Lang Header.

## Examples

```java
String s = "abc"
Object o = null
Int i = 10
Boolean b = false
Person p = Person(name: "Frank", age: 30)
```