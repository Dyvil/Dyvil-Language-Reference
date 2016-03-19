# Statements

```sh
statement : statementList | ifStatement | whileStatement | doStatement
          | forStatement | syncStatement | tryStatement | bytecode
          | throwStatement | branchStatement

statementList : '{' '}'
              | '{' statementListElement { semi statementListPart } '}'
statementListPart : label? ( expression | variable )
label : identifier ':'
variable : ( variableModifier | annotation )? type identifier '=' expression

ifStatement : 'if' '(' expression ')' expression
              ( semi? 'else' expression )?
whileStatement : 'while' '(' expression ')' expression
repeatStatement : 'repeat' expression semi? 'while' expression
forStatement : 'for' '(' variable? semi expression? semi expression? ')'
                expression
syncStatement : 'synchronized' '(' expression ')' expression
tryStatement : 'try' expression { catchStatement } finallyStatement?
catchStatement : 'catch' '(' variable ')' expression
finallyStatement : 'finally' expression
throwStatement : 'throw' expression

branchStatement : breakStatement | continueStatement | gotoStatement
breakStatement : 'break' identifier?
continueStatement : 'continue' identifier?
gotoStatement : 'goto' identifier
```