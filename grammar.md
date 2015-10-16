# Grammar

The following pages contain a formal description of the Dyvil grammar. The production rules are provided in a format shown below.

# Grammar Format

- Rules: Rules are written in the form `name : value` and can be referenced by name.
- Literals: Literal Tokens are denoted with `''` or `""`.
  Example: `myRule : myRule '.' myRule`
- Optionals: Optional Tokens or Expressions are denoted with a postfix `?` or surrounded by square brackets `[ ]`.
  Example: `myRule : '1'? myRule`
- Lists: Repeated token sequences that are valid once or more are denoted with `{}`.
  Example: `octalNum : '0x'? octal { octal }`
- Variations: Variations are either denoted with `|` or by defining the same rule multiple times.
- Exclusions: If a rule or literal should not be matched, it can be excluded with `^`.
  Example: `charLiteral : "'" { any ^ "'" }? "'"`

# Note

Please note that this is not an exact representation of the Dyvil grammar. It does not account for Semicolon Inference or operator precedence, as these are context-dependent and cannot easily be represented in a formal grammar. Furthermore, it might be possible that the actual Dyvil parser as used by the Dyvil Compiler accepts a wider grammar, and would not raise an error in cases in which a parser built from this grammar would.