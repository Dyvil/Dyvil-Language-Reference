# Lexical Syntax

The following pages describe the Lexical Syntax of Dyvil Files.

## Semicolon Inference

Much like in Java, statements have to be terminated using semicolons `;`, usually at the end of a line. In Dyvil however, these semicolons can be omitted in many cases. This is because of a process known as Semicolon Inference, which happens before the Compiler parses Dyvil Files.

**Example**:

```java
public class MyClass
{
    public int value = 0    // ;
    
    public static void main([String] args)
    {
        int i = 10          // ;
        println i           // ;
        i *= 2              // ;
        println i           // ;
        if (i >= 20)        // 1
        {
            println "\(i) is greater than 20!" // ;
        }
        
        auto my = new MyClass   // ;
        
        println(                // 2
                my,             // 3
                my.             // 4
                    value
                "value")
        
        println;                // 5
        
        println "\(             // 6
                    my)
    }
}
```

In the above example, semicolons are implicit in all cases where they are shown in comments. The parses notices that the statement is finished and a newline is present, and thus inserts a semicolon for you. While this usually happens at the end of a line, there are a few exceptions.

Semicolons are __not__ inserted if

- the first token in the next line is an opening curly bracket `{` (1)
- the last token before the newline is
    - an opening bracket `(`, `[` or `{` (2)
    - a period `.` (3)
    - a comma `,` (4)
    - a semicolon `;` (5)
    - a part of a String Interpolation literal (6)
    