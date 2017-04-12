---
dyvil: v0.31.0
---

# Properties

It is common practice to encapsulate fields of a class by making them `private` and providing getters and setters. Because this is so widely used in the Java world, Dyvil provides special syntax to simplify the declaration of properties.

```swift
class Person
{
    private var _name: String
    
    var name: String // properties are implicitly public
    {
        init: this._name = ""
        get: this._name // getter returns value stored in the _name field
        set: this._name = newValue // setter stores the parameter value in the _name field
    }
}
```

In this example, the property body consists of three parts, the **`get`ter**, **`set`ter** and **`init`ializer**. All three can use either colon syntax or statement lists:

```swift
var name: String // properties are implicitly public
{
    init { this._name = "" }
    get { this._name } // getter returns value stored in the _name field
    set { this._name = newValue }// setter stores the parameter value in the _name field
}
```

## The getter: `get`

The getter provides the means of receiving the value of the property. It generates a method of the following form:

```swift
<modifiers+annotations> func name() -> Type = body
```

In the above example, this would be

```swift
/* public */ func name() -> String = this._name
```

## The setter: `set`

The setter is called when assigning a value to the property. The generated method looks like this:

```swift
<modifiers+annotations> func name_=(newValue: Type) -> void = body
```

For the `Person.name` property, the generated method would look like this:

```swift
/* public */ func name_=(newValue: String) -> void = this._name = newValue
```

The name of the setter parameter is usually `newValue`, but it can be customized by adding the desired name in parentheses after the `set` keyword:

```swift
var name: String
{
    get: ...
    set(newName): this._name = newName
}
```

## The initializer: `init`

Although it is rarely required in practice, properties can be initialized when an object is created or a class is loaded. This can be achieved with the `init` keyword, as shown the `Person` class. The initializer expression has to be usable as a statement. Initializers of `static` properties run when the class is loaded; instance properties are initialized when an object of the class is constructed.

Getters and setters may also have additional modifiers and annotations, like `abstract` or `final`. The modifiers and annotations of the property are applied to both getter and setter. In the context of properties, `final` means non-overridable instead of non-reassignable. As a result of this, a property cannot be declared with the `let` keyword, only using `var`.

## Field Properties

Fields in class contexts may define inline property getters and setters. They are automatically used when accessing or assigning to that field.

```swift
class Foo
{
    var i: int = 0 { get; set }
}
```

is equivalent to

```swift
class Foo
{
    var i = 0 // field

    var i: int // property
    {
        get: this.i
        set: this.i = newValue
    }
}
```

If the `get` or `set` keywords are used within the property body, the compiler generates default accessors as shown above. To allow as much flexibility as possible, this can be overriden with the usual property syntax.

```swift
class Foo
{
    var i = 0
    {
        get
        {
            print "get"
            return i
        }
        set
        {
            print "set \(newValue)"
            i = newValue
        }
    }
}

var foo = new Foo
print foo.i       // prints 'get', '0'
foo.i = 2         // prints 'set 2'
```



