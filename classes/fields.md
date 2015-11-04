# Fields

Fields are a way to store information about objects of a certain class. They are created with the same notation as in Java:

```java
class Person
{
    String name
    int age = 20
]
```

## Modifiers

Fields can be annotated with a variety of modifiers. Apart from standard visibility modifiers, the following field-specific modifiers can be used:

- `final`

  The final modifier makes a field immutable. This means it cannot be re-assigned after it has been set to an initial value.
  
  ```java
  final String name
  
  public void setName(String newName)
  {
      this.name = newName // illegal
  }
  ```
  
- `lazy`

  The lazy modifier tells the compiler that a field should be initialized lazily, i.e. when it is used for the first time.
  
  ```java
  String myString = getMyString()
  lazy String myLazyString = getMyString()
  
  static String getMyString()
  {
      println "getMyString()"
      return "Hello World"
  }
  
  {                         // prints 'getMyString()' during
                            // initialization of 'myString'
      println "Starting..." // prints 'Starting...'
      println myString      // prints 'Hello World'
      println myLazyString  // prints 'getMyString()' and then 'Hello World'
      println myLazyString  // prints 'Hello World'
  ]
  ```