---
dyvil: v0.34.0
---
# Top-Level Declarations

## Dyvil Files

```sh
# *.dyv, *.dyvil
unit : package? { headerPart semi }? headerDeclaration? { classDeclaration }?
# *.dyh, *.dyvilh
header : package? { headerPart semi }? headerDeclaration?

package : 'package' identifier { '.' identifier }? semi
```

## Headers

```sh
headerDeclaration : { accessModifier | annotation }? 'header' identifier
headerPart : import | using | operatorDeclaration | typeAlias

import : 'import' importPart
using : 'using' importPart
importPart : importQualifier { identifier '.' }? importEnd
importEnd : namedImport | multiImport | packageImport
namedImport : identifier ( '=>' identifier )?
multiImport : '{' '}' | '{' importPart { comma importPart }? '}'
packageImport : '_'
importQualifier : 'package' | 'header' | 'operator' | 'type'
                | 'class' | 'static' | 'var' | 'const' | 'let'
                | 'func' | 'inline' | 'implicit'

operatorDeclaration : simpleOperator | ternaryOperator
simpleOperator : operatorType 'operator' operatorSymbol operatorProperties?
ternaryOperator : 'infix' 'operator' operatorSymbol operatorSymbol operatorProperties? 
operatorType : 'prefix' | 'postfix' | 'infix'
operatorSymbol : identifier | '=' | ':'

operatorProperties : '{' '}' | '{' operatorProperty { ',' operatorProperty }? '}'
operatorProperty : 'precedence'? precedence
                 | 'associativity'? associativity
precedence : int
associativity : 'none' | 'left' | 'right'

typeAlias : 'type' identifier typeVariables? '=' type
```

## Attributes

```sh
modifier : 'public' | 'package' | 'protected' | 'private'
         | 'deprecated' | 'internal' | 'final' | 'static'
         | 'abstract' | 'case' | 'functional' | 'sealed'
         | 'prefix' | 'postfix' | 'infix' | 'inline'
         | 'synchronized' | 'override' | 'final' | 'lazy'

modifiers : { modifier }?

annotation : '@' type arguments?
annotations : { annotation }?

attributes : { modifier | annotation }?
```

## Classes

```sh
classDeclaration : modifiers classKind identifier
                   typeVariables? parameters?
                   extendsClause? implementsClause?
                   ( classBody | semi )

classKind : 'class' | 'enum' | 'object' | 'extension'
          | 'interface' | '@' 'interface' | 'trait'
extendsClause : 'extends' type arguments?
implementsClause :  'implements' type { comma type }?

typeVariables : '<' '>' | '<' typeVariable { comma typeVariable }? '>'
typeVariable : annotations 'type'? variance? identifier bounds?
bounds : ( 'extends' | ':' ) type { '&' type }?
variance : '+' | '-'

typeAscription : ':' type

parameters : '(' ')' | '(' parameter { comma parameter }? ')'
parameter : attributes ('var' | 'let')?
            identifier parameterType
            ( '=' expressionNoClosure )? propertyBody?
parameterType : ellipsis
              | ellipsis typeAscription
              | typeAscription
              | typeAscription ellipsis

classBody : '{' { member semi }? '}'
member : field | property | method | constructor | initializer

field : attributes ('var' | 'let' | 'const') identifier typeAscription? ( '=' expressionNoClosure propertyBody?)?

property : attributes 'var' identifier
           typeAscription? propertyBody
propertyBody : '{' propertyTag { semi propertyTag }? }
propertyTag : propertyGetter | propertySetter | propertyInit
propertyGetter : modifiers 'get' propertyStatement
propertySetter : modifiers 'set' propertySetterName? propertyStatement
propertySetterName : '(' identifier ')'
propertyInit : 'init' propertyStatement
propertyStatement : ':' expression | statementList

method : attributes 'func' identifier typeVariables? parameters?
         throwsClause? typeAscription? methodExpression?

throwsClause : 'throws' type { comma type }?
methodExpression : '=' expression | statementList

constructor : attributes 'init' parameters constructorCall? throwsClause? methodExpression?
constructorCall : ':' ('this' | 'super') arguments

initializer : attributes 'init' statementList

```