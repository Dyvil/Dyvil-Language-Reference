# Types

```sh
type : namedType | genericType | null | arrayType | lambdaType | voidType | tupleType | wildcardType
namedType : identifier { '.' identifier }
genericType : namedType '[' type { comma type }? ']'
arrayType : '[' type? ']' # The type is optional because [] evaluates to [any]
lambdaType : '(' ')' '=>' type | '=>' type
lambdaType : type '=>' type | '(' type { comma type }? ')' '=>' type
voidType : '(' ')'
tupleType : '(' type { comma type }? ')'
wildcardType : '_' | '_' upperBound | '_' lowerBound

upperBounds : { '<:' type }
upperBound : '<:' type
lowerBound : '>:' type
```