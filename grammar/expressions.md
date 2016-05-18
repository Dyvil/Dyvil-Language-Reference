# Expressions

```sh
expression : expressionNoClosure | applyCall
expressionNoClosure : literal | stringInterpolation | voidValue
                    | thisExpression | superExpression | initExpression | constructor
                    | statement
                    | methodCall | fieldAccess | applyCallNoClosure | subscriptCall
                    | castExpression | instanceOfExpression
                    | classExpression | typeExpression
                    | arrayExpression | tupleExpression
                    | lambdaExpression | matchExpression
                    | braceAccessExpression | colonExpression | assignment
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

access : (expression '.'?)? ( fieldAccess | methodCall )
access : expression '.' 

fieldAccess : (expression '.')? identifier
methodCall : (expression '.')? identifier typeArguments? ( arguments | expression )
applyCall : expression arguments | expression { expression }
applyCallNoClosure : expression arguments | expression { expressionNoClosure }
subscriptCall : expression subscriptArguments

arguments : '(' ')' | '(' argumentList ')'
subscriptArguments : '[' ']' | '[' argumentList ']'
argumentList : label? expression { comma label? expression }
typeArguments : '[' type { comma type }? ']'

assignment : expression '=' expression

thisExpression : 'this' classSpecifier?
superExpression : 'super' classSpecifier?
classSpecifier : '<' type '>'

initExpression : ( 'this' '.' | 'super' '.' ) 'init' arguments

classExpression : 'class' type
                | 'class' '(' type ')'
                | 'class' '<' type '>'

typeExpression  : 'type' type
                | 'type' '(' type ')'
                | 'type' '<' type '>'

castExpression : expression 'as' type
instanceOfExpression : expression 'is' type

lambdaExpression : lambdaParameters? ('->' type)? '=>' expression
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