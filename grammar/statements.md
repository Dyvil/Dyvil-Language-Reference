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
doStatement : 'do' expression semi? 'while' expression
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

bytecode : '@' '{' '}' | '@' '{' bytecodePart { semi bytecodePart }? '}'
bytecodePart : label? instruction
```

### Bytecode Instructions

```sh
instruction : simpleInstruction | varInstruction | intInstruction
            | multiArrayInstruction | fieldInstruction | methodInstruction
            | jumpInstruction
simpleInstruction : identifier
varInstruction : identifier int int
intInstruction : identifier int
multiArrayInstruction : identifier string int
fieldInstruction : identifier internalType '.' identifier ':' internalType
methodInstruction : identifier internalType '.' identifier
                    '(' ( internalType { ',' internalType } )? ')'
                    ':' internalType
jumpInstruction : identifier identifier

internalType : identifier { '/' identifier }?
```