# Top-Level Declarations

## Dyvil Files

```sh
unit : package? { headerPart }? headerDeclaration? { classDeclaration }?
header : package? { headerPart }? headerDeclaration?

package : 'package' identifier { '.' identifier }? semi
```

## Headers

```sh
headerDeclaration : { accessModifier | annotation }? 'header' identifier
headerPart : ( include | import | using | operatorDeclaration | typeAlias ) semi

include : 'include' identifier { '.' identifier }?
import : 'import' importPart
using : 'using' importPart
importPart : { identifier '.' }? importEnd
importEnd : identifier ( '=>' identifier )?                  # Named Import
importEnd : '{' '}' | '{' importPart { ',' importPart }? '}' # Multi-Import
importEnd : '_'                                              # Package Import

operatorDeclaration : operatorType 'operator' identifier operatorProperties?
operatorType : 'prefix' | 'postfix' | 'infix'

operatorProperties : '{' operatorProperty { ',' operatorProperty }? '}'
operatorProperty : 'precedence'? precedence
operatorProperty : 'associativity'? associativity
precedence : int
associativity : 'none' | 'left' | 'right'

typeAlias : 'type' typeVariables? identifier '=' type
```

## Classes

```sh
modifier : classModifier | methodModifier | fieldModifier
accessModifier : 'public' | 'package' | 'protected' | 'private' | 'deprecated' | 'internal'
classModifier : accessModifier | 'final' | 'static' | 'abstract' | 'case' | 'functional' | 'sealed'
methodModifier : accessModifier | 'final' | 'static' | 'abstract' | 'prefix' | 'postfix' | 'infix' | 'inline' | 'synchronized' | 'override'
fieldModifier : accessModifier | 'final' | 'const' | 'lazy'
parameterModifier : 'lazy' | 'final' | 'var'
variableModifier : 'lazy' | 'final'
classKind : 'class' | 'enum' | 'object' | 'interface' | '@' 'interface' | 'extension'

classDeclaration : { classModifier | annotation }? classKind identifier
    typeVariables? parameters? extendsClause? implementsClause? ( classBody | semi )

extendsClause : 'extends' type
implementsClause :  'implements' type { comma type }?

annotation : '@' identifier annotationArguments?
annotationArguments : arrayExpression | arguments

typeVariables : '[' ']' | '[' typeVariable { comma typeVariable }? ']'
typeVariable : variance? identifier upperBounds?
variance : '+' | '-'

parameters : '(' ')' | '(' parameter { comma parameter }? ')'
parameter : { parameterModifier | annotation }? type identifier ellipsis? { '=' expression }

classBody : '{' { member semi }? '}'
member : field | property | method | constructor

field : { fieldModifier | annotation }? type identifier ( '=' expression )?

property : { fieldModifier | annotation }? type identifier '{' ( getterClause setterClause? | setterClause getterClause? ) '}'
getterClause : { fieldModifier }? 'get' ':' expression
setterClause : { fieldModifier }? 'set' ':' expression

method : { methodModifier | annotation }? type identifier typeVariables? parameters throwsClause? methodExpression?
throwsClause : 'throws' type { comma type }?
methodExpression : '=' expression | statementList

constructor : { methodModifier | annotation }? 'new' parameters throwsClause? methodExpression?

```