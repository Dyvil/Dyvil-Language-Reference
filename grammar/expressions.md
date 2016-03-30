# Expressions

```sh
expression : literal | stringInterpolation | voidValue
           | thisExpression | superExpression | initExpression
           | statement | access | assignment | constructor
           | castExpression | instanceOfExpression
           | classExpression | typeExpression
           | arrayExpression | tupleExpression
           | lambdaExpression | matchExpression
           | braceAccessExpression | colonExpression
```

## Simple Expressions

```sh
literal : number | stringLiteral | charLiteral | boolean | null | nil
voidValue : '(' ')'

stringInterpolation : stringStart expression { stringPart expression }? stringEnd
```

## Compound Expressions

```sh

arrayExpression : '[' ']' | '[' expression { comma expression }? ']'
tupleExpression : '(' expression { comma expression }? ')'
colonExpression : expression ':' expression

constructor : 'new' type arguments? classBody?

access : (expression '.'?)? ( fieldAccess | methodCall | applyCall | subscriptCall )
fieldAccess : identifier
methodCall : identifier ( arguments? | expression )
applyCall : arguments
subscriptCall : expression subscriptArguments

arguments : '(' ')' | '(' argumentList ')'
subscriptArguments : '[' ']' | '[' argumentList ']'
argumentList : '(' label? expression { comma label? expression } ')'

assignment : access '=' expression

thisExpression : 'this' ( '[' type ']' )?
superExpression : 'super' ( '[' type ']' )?

initExpression : ( 'this' '.' | 'super' '.' ) 'init' arguments

classExpression : 'class' type
                | 'class' '(' type ')'

typeExpression  : 'type' type
                | 'type' '(' type ')'

castExpression : expression 'as' type
instanceOfExpression : expression 'is' type

matchExpression : expression '.'? 'match' matchBody
matchBody : caseExpression | '{' { caseExpression }? '}'

lambdaExpression : lambdaParameters? '=>' expression
lambdaParameters : parameters | identifier

braceAccessExpression : expression '.' statementList
```

## Patterns

```sh
pattern : orPattern { '&' orPattern }
orPattern : primaryPattern { '|' primaryPattern }
primaryPattern : literal | '-' number | '_' | bindingPattern
               | tuplePattern | classPattern | typeCheckPattern
bindingPattern : 'var' identifier | type identifier
typeCheckPattern : pattern 'as' type
tuplePattern : '(' pattern { comma pattern }? ')'
classPattern : type classPatternArguments?
classPatternArguments : '(' ')' | '(' pattern { comma pattern }? ')'
```