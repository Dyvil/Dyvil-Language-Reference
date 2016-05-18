# Types

The Type system is way more advanced and extensive than in Java. Dyvil introduces a variety of different sorts of types:

1. The base type of everything - `any`
2. The type of the `null` literal - `null`
3. Dynamic Types - `dynamic`
4. Primitive Types - `int`
5. Object Types - `String`, `Date`, `Object`
6. Generic Types - `List[int]`, `List[Option[Date]]`
7. Tuple Types - `(int, String)`
8. Function Types - `(int, int) -> int`
9. Type Variable Types - `T`
10. Wildcard Types - `_`, `_ <: Number`
11. Reference Types - `int*`, `String*`, `any^`
12. Option Types - `int?`, `String?`, `long!`, `List[String]!`