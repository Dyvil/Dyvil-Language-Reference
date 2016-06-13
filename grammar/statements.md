# Statements

```sh
statement : statementList | ifStatement | whileStatement | repeatStatement
          | forStatement | forEachStatement | syncStatement | tryStatement | bytecode
          | throwStatement | branchStatement

statementList : '{' '}'
              | '{' statementListPart { semi statementListPart } '}'
statementListPart : label? ( expression | member )
label : identifier ':'

variable : { fieldModifiers | annotation }? ( type | 'var' )? identifier typeAscription?

ifStatement : 'if' expressionNoClosure ':'? expression
                   ( semi? 'else' expression )?

matchExpression : expression '.'? 'match' matchBody
                | 'match' expressionNoClosure ':'? matchBody
matchBody : caseExpression | matchCompound
matchCompound : '{' { caseExpression }? '}'

whileStatement : 'while' expressionNoClosure ':'? expression

repeatStatement : 'repeat' expression semi? 'while' expression

forStatement : 'for' '(' ( variable '=' expression )? semi expression?
               semi expression? ')' expression
             | 'for' ( variable '=' expression )? semi expression?
               semi expressionNoClosure? statementList
             
forEachStatement : 'for' '(' variable '<-' expression ')' expression
                 | 'for' variable '<-' expressionNoClosure statementList
                 | 'for' variable '<-' expressionNoClosure ':' expression

syncStatement : 'synchronized' expressionNoClosure ':'? expression

tryStatement : 'try' expression { catchStatement } finallyStatement?
catchStatement : 'catch' '(' variable ')' expression
               | 'catch' variable statementList
finallyStatement : 'finally' expression

throwStatement : 'throw' expression

branchStatement : breakStatement | continueStatement | gotoStatement
breakStatement : 'break' identifier?
continueStatement : 'continue' identifier?
gotoStatement : 'goto' identifier
```