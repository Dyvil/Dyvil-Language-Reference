---
dyvil: v0.34.0
---
# Statements

```sh
statement : statementList | ifStatement | whileStatement | repeatStatement
          | forStatement | forEachStatement | syncStatement | tryStatement | bytecode
          | throwStatement | jumpStatement

statementList : '{' '}'
              | '{' statementListPart { semi statementListPart } '}'
statementListPart : label? ( expression | member )
label : identifier ':'

variableDeclaration : attributes? ( 'var' | 'let' ) identifier typeAscription?
variable : variableDeclaration '=' expression

ifStatement : 'if' expressionNoClosure expression
                   ( semi? 'else' expression )?

matchExpression : expression '.'? 'match' matchBody
                | 'match' expressionNoClosure matchBody
matchBody : caseExpression | caseList
caseList : '{' '}' '{' caseExpresssion { semi caseExpression }? '}'
# caseExpression is declared in Expressions/Patterns

whileStatement : 'while' expressionNoClosure expression

repeatStatement : 'repeat' expression semi? 'while' expression

forStatement : 'for' '(' variable? semi expression?
               semi expression? ')' expression
             | 'for' variable semi expression?
               semi expressionNoClosure? statementList
             
forEachStatement : 'for' '(' variableDeclaration '<-' expression ')' expression
                 | 'for' variableDeclaration '<-' expressionNoClosure statementList

syncStatement : 'synchronized' expressionNoClosure expression

tryStatement : 'try' expression { catchStatement } finallyStatement?
catchStatement : 'catch' '(' variableDeclaration ')' expression
               | 'catch' variableDeclaration statementList
finallyStatement : 'finally' expression

throwStatement : 'throw' expression

jumpStatement : breakStatement | continueStatement | gotoStatement
breakStatement : 'break' identifier?
continueStatement : 'continue' identifier?
gotoStatement : 'goto' identifier
```