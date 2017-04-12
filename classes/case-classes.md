---
dyvil: v0.32.0
---

# Case Classes

Case Classes are a syntactic sugar that allows you to save a lot of boilerplate code. Consider the following Java class:

```java
class Book
{
    String name;
    String author;
    final int id;

    public Book(String name, String author, int id)
    {
        this.name = name;
        this.author = author;
        this.id = id;
    }
```

Simple enough, though you may also need an `equals`, `hashCode` and `toString` implementation.

```java
    public String toString()
    {
        return "Book(" + this.name + ", " + this.author + ", " + this.id + ")";
    }

    public boolean equals(Object other)
    {
        if (!(obj instanceof Book)) return false;

        final Book otherBook = (Book) other;
        if (this.name != otherBook.name || this.name == null || !this.name.equals(otherBook.name)
            return false;
        if (this.author != otherBook.author || this.author == null || !this.author.equals(otherBook.author)
            return false;
        if (this.id != otherBook.id)
            return false;

        return true;
    }

    public int hashCode()
    {
        final int prime = 31;
        int result = 1;
        result = prime * result + (this.name == null ? 0 : this.name.hashCode());
        result = prime * result + (this.author == null ? 0 : this.author.hashCode());
        result = prime * result + this.id;
        return result;
    }
}
```

For a class as simple as the `Book` class, this is a lot of boilerplate. Although IDEs might help you with this by generating the boilerplate code for you, maintaining it still costs a lot of time. In Dyvil, the compiler can generate all this code by using the `case` class modifier:

```java
case class Book(var name: String, var author: String, let id: int)
```

In addition to all methods in the Java class above, a Case Class generates a static `apply` method that can be used to construct instances:

```swift
// generated in the Book class:
static func apply(name: String, author: String, id: int) -> Book = new Book(name, author, id)

// usage:
let book = Book("The Dyvil Language Reference", "Dyvil Team", 0xCAFEBABE)
```

Case Classes provide extensive support for use in [Pattern Matching](../expressions/patterns.md) by generating two different `unapply` methods:

```swift
// generated in the Book class:
static func unapply(value: any) -> (String, String, int)? = value is Book ? unapply(value as Book) : null
static func unapply(value: Book) -> (String, String, int) = (value.name, value.author, value.id)

// usage:
book match {
    // match a book with any name, the author "Dyvil Team" and any id and store the name
    case Book(var name, "Dyvil Team", _) => print name
}
```



