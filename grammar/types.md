---
dyvil: v0.34.0
---
# Types

```sh
type : typeNoVoid | voidType
typeNoVoid : namedType | genericType | nullType | arrayType
           | lambdaType | tupleType | wildcardType | infixType
           | prefixType | postfixType

types : type { comma type }?

namedType : identifierList
genericType : namedType '<' types? '>'
```

## Basic Types

```sh
nullType : 'null'
voidType : '(' ')'
wildcardType : '_'
```

## Collection Types

```sh
mutability : 'var' | 'final'

tupleType : '(' types ')'
arrayType : '[' mutability? type? ']'
          | type '[' ']' # Java-Style, causes warning
mapType   : '[' mutability? type ':' type ']'
```

## Compound Types

```sh
lambdaType : '=>' type
           | typeNoVoid '=>' type
           | '(' types? ')' '=>' type
           | type '.' '(' types? ')' '=>' type

infixType : type identifier type
prefixType : identifier type
postfixType : type identifier
```