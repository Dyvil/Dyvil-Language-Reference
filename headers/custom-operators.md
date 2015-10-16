# Custom Operators

Custom Operators can be defined in Header Files or in the header of a class file. Note that it is not possible to define custom operators anywhere else.

The following syntax is used to define a custom operator:

1. The type of operator
    - `infix`
    - `prefix`
    - `postfix`
2. The keyword `operator`
3. The name
4. An optional list of additional comma-separated properties in curly brackets.
    - `precedence` + integer literal
    - `associativity`
        - `none`
        - `left`
        - `right`

Example:

```swift
prefix operator  &
postfix operator ^
```

`infix` operators also need additional properties to be fully defined, namely a `precedence` value and an `associativity` type.

You can define these properties in curly brackets after the name of the operator:

```swift
infix operator +- { none,             120 }
//                  ^ associativity   ^ precedence 
```

It is optional, but recommended for clarity, to type out which property is being defined:

```swift
infix operator +- { associativity none, precedence 120 }
infix operator +- { associativity none,            120 }
infix operator +- {               none, precedence 120 }
```

The order in which the properties are placed within the brackets does not matter.