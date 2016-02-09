# Top-Level Declarations

## Dyvil Files

```sh
unit : package? { headerPart semi }? headerDeclaration? { classDeclaration }?
header : package? { headerPart semi }? headerDeclaration?

package : 'package' identifier { '.' identifier }? semi
```

## Headers

```sh
headerDeclaration : { accessModifier | annotation }? 'header' identifier
headerPart : include | import | using | operatorDeclaration | typeAlias

include : 'include' identifier { '.' identifier }?
import : 'import' importPart
using : 'using' importPart
importPart : { identifier '.' }? importEnd
importEnd : namedImport | multiImport | packageImport
namedImport : identifier ( '=>' identifier )?
multiImport : '{' '}' | '{' importPart { ',' importPart }? '}'
packageImport : '_'

operatorDeclaration : operatorType 'operator' identifier operatorProperties?
operatorType : 'prefix' | 'postfix' | 'infix'

operatorProperties : '{' operatorProperty { ',' operatorProperty }? '}'
operatorProperty : 'precedence'? precedence
                 | 'associativity'? associativity
precedence : int
associativity : 'none' | 'left' | 'right'

typeAlias : 'type' typeVariables? identifier '=' type
```

## Classes

```sh
modifier : classModifier | methodModifier | fieldModifier
accessModifier : 'public' | 'package' | 'protected' | 'private'
               | 'deprecated' | 'internal'
classModifier : accessModifier | 'final' | 'static' | 'abstract'
              | 'case' | 'functional' | 'sealed'
methodModifier : accessModifier | 'final' | 'static' | 'abstract'
               | 'prefix' | 'postfix' | 'infix' | 'inline'
               | 'synchronized' | 'override'
fieldModifier : accessModifier | 'final' | 'const' | 'lazy'
parameterModifier : 'lazy' | 'final' | 'var'
variableModifier : 'lazy' | 'final'


classDeclaration : { classModifier | annotation }? classKind identifier
                   typeVariables? parameters?
                   extendsClause? implementsClause?
                   ( classBody | semi )

classKind : 'class' | 'enum' | 'object' | 'extension'
          | 'interface' | '@' 'interface' | 'trait'
extendsClause : 'extends' type
implementsClause :  'implements' type { comma type }?

annotation : '@' type arguments

typeVariables : '[' ']' | '[' typeVariable { comma typeVariable }? ']'
typeVariable : variance? identifier upperBounds?
variance : '+' | '-'

parameters : '(' ')' | '(' parameter { comma parameter }? ')'
parameter : { parameterModifier | annotation }? type ellipsis? identifier
            { '=' expression }

classBody : '{' { member semi }? '}'
member : field | property | method | constructor | initializer

field : { fieldModifier | annotation }? type identifier ( '=' expression )?

property : { fieldModifier | annotation }? type identifier '{' propertyTags '}'
propertyTags : propertyTag { semi propertyTag }?
propertyTag : propertyGetter | propertySetter | propertyInit
propertyGetter : { fieldModifier }? 'get' propertyStatement
propertySetter : { fieldModifier }? 'set' ( '(' identifier ')' ) 
                 propertyStatement
propertyInit : 'init' propertyStatement
propertyStatement : ':' expression | statementList

method : { methodModifier | annotation }? type identifier
         typeVariables? parameters throwsClause? methodExpression?
         throwsClause : 'throws' type { comma type }?
methodExpression : '=' expression | statementList

constructor : { methodModifier | annotation }? 'new' parameters throwsClause? methodExpression?

initializer : { methodModifier | annotation }? 'init' statementList

```