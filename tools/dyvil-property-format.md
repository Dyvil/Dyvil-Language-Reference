# The Dyvil Property Format

The **Dyvil Property Format** is a JSON-like text-based configuration file format mainly designed for the [Dyvil Window Toolkit](https://github.com/Dyvil/Dyvil-Window-Toolkit).  
The format is based on two fundamental concepts: Nodes and Properties. Nodes allow you to change the properties of an existing value, while properties let you assign a value to a key.

# Values

Values provide the atomic building parts of the Dyvil Property Format. There are seven types of values in the format, all of which behave exactly the same as in Dyvil itself.

* Identifiers

```
name = dyvil
package = test
// including booleans
visible = true
enabled = false
```

* Integers

```
int10 = 123
int16 = 0xCAFEBABE
int2 = 0b1010
int8 = 0o7712
```

* Floats

```
float = 0.123
float = 0.123F
float = 0.123D
float = 2e10F
```

* Strings

```
string = "Hello World"
string = 'c'
string = "\n\n"
```

* Lists

```
list = [ 1, 2, 3 ]
list = [ "a", [ "nested, "list" ] ]
```

* Maps

```
map = { "a" : "A", "b" : "B" }
map = { name : "map", type : map, size : 3 }
```

# Nodes

Nodes represent existing values, and the block in a node expression contains more nodes and properties which are meant to be applied to the node head.

```
gui { // <- node head
  window {
    width = 500
    height = 300
  }
}
```

The `window` property is retrieved from the `gui` root property, and the `width` and `height` properties of the `window` property is assigned in the nested block.  
Putting this example in the Dyvil perspective, it is equivalent to the following code:

```
GUI gui = ...
Window window = gui.window
window.width = 500
window.height = 300
```

# Properties

Properties are simple assignments of values to keys. They can only be used within nodes or builder blocks and are dependant on the context in which they occur. In the above example, `width = 500` and `height = 300` represent the properties `width` and `height` with their corresponding values.

# Node Access

Node Access Expressions allow flattening the node structure. For example,

```
gui {
  window {
    width = 500
    height = 300
  }
}
```

Can be simplified to

```
gui.window {
   width = 500
   height = 300
}
```

Or even

```
gui.window.width = 500
gui.window.height = 300
```

Analogously, any Node Access Expression can be converted to a slightly more verbose Node:

```
library.version = "1.0.0"
library { version = "1.0.0" }
```

# Builders

Builders are a special form of values. They could be described as constructors in Dyvil terms, but have a much more elegant syntax.

```
button = Button {
  text = "Click Me"
}
```

In the above example, `Button` represents a builder for the `Button` type. All properties in the block are applied to the newly created `Button` object. The code is the Dyvil Property Format equivalent of the Dyvil code

```
button = new Button
button.text = "Click Me"
```

Builders can also use parenthesis to shorten the constructor. As with method calls in Dyvil, the parameter names may also be stated explicitly:

```
color = Color(255, 255, 255)
color = Color(r: 255, g: 127, b: 127)
```

Furthermore, it is possible to mix parenthesis with blocks:

```
button = Button(text: "Click Me") {
  visible = false
}
```



