# Types

```sh
typeList : type { comma type }?

type : namedType | genericType | nullType | arrayType | lambdaType | voidType
     | tupleType | wildcardType | optionType | implicitOptionType
     | referenceType | implicitReferenceType
namedType : identifierList
genericType : namedType '[' typeList? ']'

voidType : '(' ')'
arrayType : '[' mutability? type? ']'
          | type '[' ']'              # Java-Style Warning
lambdaType : '=>' type
           | type '=>' type
           | '(' ')' '=>' type
           | '(' type { comma type }? ')' '=>' type
           | type . lambdaType

tupleType : '(' type { comma type }? ')'
wildcardType : '_' | '_' upperBound | '_' lowerBound

optionType            : type '?'
implicitOptionType    : type '!'
referenceType         : type '*'
implicitReferenceType : type '^'

mapType : '[' mutability? type ':' type ']'
listType : '[' mutability? type '...' ']'

mutability : 'var' | 'final'

upperBounds : { upperBound }
upperBound : '<:' type
lowerBound : '>:' type
```