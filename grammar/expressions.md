# Expressions

```sh
expression : literal | stringInterpolation | voidValue | thisExpression | superExpression
expression : statement | access | assignment | constructor | castExpression | instanceOfExpression
expression : classExpression | typeExpression
expression : arrayExpression | tupleExpression
expression : lambdaExpression | matchExpression | caseExpression
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

constructor : 'new' type arguments? classBody?

access : (expression '.'?)? ( fieldAccess | methodCall | applyCall | subscriptCall )
fieldAccess : identifier
methodCall : identifier ( arguments? | expression )
applyCall : arguments
subscriptCall : expression subscriptArguments

arguments : emptyArguments | argumentList | namedArguments
emptyArguments : '(' ')'
argumentList : '(' expression { ',' expression } ')'
namedArguments : '(' label expression { ',' label expression } ')'

subscriptArguments : '[' ']' | subscriptArgumentList | namedSubscriptArguments
subscriptArgumentList : '[' expression { ',' expression } ']'
namedSubscriptArguments : '[' label expression { ',' label expression } ']'

assignment : access '=' expression

thisExpression : 'this' ( '[' type ']' )?
superExpression : 'super' ( '[' type ']' )?

classExpression : 'class' type
typeExpression : 'type' type

castExpression : expression 'as' type
instanceOfExpression : expression 'is' type

matchExpression : expression '.'? 'match' matchBody
matchBody : caseExpression | '{' { caseExpression }? '}'
caseExpression : 'case' pattern ( 'if' expression )? ( ':' | '=>' ) expression

lambdaExpression : lambdaParameters? '=>' expression
lambdaParameters : parameters | identifier | '(' identifier { comma identifier }? ')'
```

## Patterns

```sh
pattern : literal | '_' | bindingPattern | tuplePattern | classPattern | typeCheckPattern
bindingPattern : 'var' identifier
typeCheckPattern : pattern 'as' type
tuplePattern : '(' pattern { comma pattern }? ')'
classPattern : identifier classPatternArguments?
classPatternArguments : '(' ')' | '(' pattern { comma pattern }? ')'
```