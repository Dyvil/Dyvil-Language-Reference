# Operators


Through **Operators**, Dyvil provides a way to override existing operators and define new operators. In Dyvil, there is no clear distinction between an alphanumerical identifier such as `fooBar123` and an operator with symbols like `+`, `+:-` or `*\*`. That means one could easily name a method with an operator name without any problems, as shown below

```scala
infix int +-(int i, int j) = i + -j
1 +- 2 // -1
```

To be JVM-compatible, the compiler replaces all operators in these identifiers according to the following table:

| Symbol | Replacement |
|--------|-------------|
| =      | $eq         |
| +      | $plus       |
| -      | $minus      |
| *      | $times      |
| /      | $div        |
| \      | $bslash     |
| %      | $percent    |
| #      | $hash       |
| @      | $at         |
| <      | $lt         |
| >      | $gt         |
| :      | $colon      |
| .      | $dot        |
| !      | $bang       |
| ?      | $qmark      |
| ~      | $tilde      |
| ^      | $up         |
| &      | $amp        |
| &#124; | $bar        |

For example, a method with the operator name `+*` has the name `$plus$times` when accessed from Java.