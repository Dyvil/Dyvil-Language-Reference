---
dyvil: v0.34.0
---
# Dyvil Property Format

The following page describes the grammar of the Dyvil Property Format. Please consult the [Grammar](grammar.md) page to find out about the format of this grammar definition as well as character classes and tokens.

## Node Elements

```sh
dpfFile : nodeElements

nodeElement : property | node | access
nodeElements : { nodeElement }
nodeElementList : '{' '}' | '{' nodeElements '}'

property : identifier ('=' | ':') value
access : identifier '.' nodeElement
node : identifier nodeElementList
```

## Values

```sh
value : literal | identifier | list | map | builder
literal : number | stringLiteral | charLiteral | boolean | null

list : '[' ']' | '[' value { ',' value }? ']'
map : '{' '}' | '{' mapEntry { ',' mapEntry }? '}'
mapEntry : value ':' value

builder : identifier parameterList? nodeBody?

parameter : (identifier ':')? value
parameterList : '(' ')' | '(' parameter { ',' parameter }? ')'
```