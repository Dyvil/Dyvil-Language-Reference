---
dyvil: v0.34.0
---

# Tokens

## Character Classes

```sh
any : '\0' .. '\uFFFF'

binary : '0' | '1'
decimal : '0'..'9'
octal : '0'..'7'
hexadecimal : '0'..'9' | 'a'..'f' | 'A'..'F'

alpha : 'a'..'z' | 'A'..'Z'
symbol : '=' | '>' | '<' | '+' | '-' | '*' | '/' | '!'
       | '@' | '#' | '%' | '^' | '&' | '~' | '?' | '|'
       | '\' | ':'

nl : "newline character"
semi : ';' | nl { nl }?
comma : ',' | nl { nl }?
```

## Tokens

```sh
comment : lineComment | multiLineComment | docComment
lineComment : '//' { any ^ nl } nl
multiLineComment : '/*' { any ^ '*/' } '*/'
docComment : '/**' { any ^ '*/' } '*/'

identifier : { '.' }? identifierSeparator? identifierPart { identifierSeparator identifierPart }?
identifier : '`' (any ^ '`') '`'
identifierSeparator : '_' | '$'
identifierPart : alphaIdentifier | symbolIdentifier
alphaIdentifier : alpha { alpha | decimal }?
symbolIdentifier : symbol { symbol }?

# Special Identifiers

dot : '.'
wildcard : '_'
ellipsis : '...'
null : 'null'
nil : 'nil'
boolean : 'true' | 'false'

number : int | long | float | double

int : binaryNum | octalNum | decimalNum | hexNum
binaryNum : '0b' binary { binary }?
octalNum : '0o' octal { octal }?
decimalNum : decimal { decimal }?
hexNum : '0x' hexadecimal { hexadecimal }?
long : int 'l' | int 'L'

floatingNum : decimalNum | decimalNum '.' decimalNum
float : floatingNum 'f' | floatingNum 'F'
double : floatingNum | floatingNum 'd' | floatingNum 'D'

charLiteral : "'" { any ^ "'" }? "'"
stringLiteral : '"' { any ^ '"' }? '"'
stringLiteral : stringStart

stringStart : '"' { any ^ "\(" }            # Enables String Interpolation Mode
stringPart : ')' { any ^ '"' ^ '\(' } '\('  # If String Interpolation Mode is on
stringEnd : ')' { any ^ '"' } '"'           # If String Interpolation Mode is on

verbatimString = '@"' { any ^ '"' } '"'
```



