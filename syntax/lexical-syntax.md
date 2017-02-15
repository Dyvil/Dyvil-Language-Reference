# Lexical Syntax

The following pages describe the Lexical Syntax of Dyvil Files.

## Semicolon Inference

Much like in Java, statements have to be terminated using semicolons `;`, usually at the end of a line. In Dyvil however, these semicolons can be omitted in many cases. This is because of a process known as Semicolon Inference, which happens before the Compiler parses Dyvil Files.

**Example**:

```java
public class MyClass
{
    public var value: int = 0   // ;
    
    static func main(args: [String]) -> void
    {
        var i = 10              // ;
        print i                 // ;
        
        let my = new MyClass    // ;
        
        print(                  // 1
                my,             // 2
                my.             // 3
                    value,
                "value")        // ;
        
        print;                  // 4
        
        print "\(               // 5
                    my)         // ;
        
        if (i >= 20)            // 6
        {
            print "\(i) is greater than 20!" // ;
        }
    }
}
```

In the above example, semicolons are implicit in all cases where they are shown in comments. The parses notices that the statement is finished and a newline is present, and thus inserts a semicolon for you. While this usually happens at the end of a line, there are a few exceptions.

Semicolons are __not__ inserted if

- the last token before the newline is
    - an opening bracket `(`, `[` or `{` (1).
    - a period `.` (2).
    - a comma `,` (3).
    - a semicolon `;` (4).
    - a keyword, excluding
        - `true` and `false`.
        - `break` and `continue`.
        - `this` and `super`.
    - the start or a part of a String Interpolation Literal (5).
- the first token of the next line is
    - a period `.`.
    - a comma `,`.
    - a semicolon `;`.
    - a part or the end of a String Interpolation Literal.
    - an opening curly bracket `{` (6).
    - a closing bracket `)`, `]` or `}`.

If there is one or more empty lines between two tokens, a semicolon will always be inserted between them.
    