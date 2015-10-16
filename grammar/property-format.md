# Dyvil Property Format

The following page describes the grammar of the Dyvil Property Format. Please consult the [Grammar](grammar.md) page to find out about the format of this grammar definition as well as character classes and tokens.

## Node Elements

```sh
dpfFile : { nodeElement }

nodeElement : property | node | access

property : identifier '=' value
access : identifier '.' nodeElement
node : identifier nodeBody
nodeBody : '{' { nodeElement } '}'
```

## Values

```sh
value : literal | identifier | list | map | builder
literal : number | stringLiteral | charLiteral | boolean | null

list : '[' ']' | '[' value { ',' value }? ']'
map : '{' '}' | '{' value ':' value { ',' value ':' value }? '}'

builder : identifier parameters? nodeBody?

parameters : '(' ')' | '(' parameter { ',' parameter }? ')'
parameter : (identifier ':') value
```