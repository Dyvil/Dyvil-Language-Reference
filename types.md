# Types

The Type system is way more advanced and extensive than in Java. Dyvil introduces a variety of different sorts of types:

1. The base type of everything - `any`
2. The type of the `null` literal - `null`
3. Dynamic Types - `dynamic`
4. Primitive Types - `int`
5. Reference Types - `String`
6. Generic Types - `List[int]`, `List[Option[Date]]`
7. Tuple Types - `(int, String)`
8. Function Types - `(int, int) => int`
9. Type Variable Types - `T`
10. Wildcard Types - `_`, `_ <: Number`

All of these types are interconnectable - a `Tuple2[Int, Int]` is the same as `(int, int)` - and comparable - a `(String, String) => any` is a super type of `(any, any) => String`. In this tutorial, all of these types will be explained in more detail.


```

##`any`, or *the* base type

Since there is no real super type of reference types and primitive types in the JVM, `any` is the semantic equivalent of `java.lang.Object`. That implies that boxing is required to correctly support primitive values. An variable such as

```java
any a = 10
```

gets converted to the slightly less performant

```java
Object a = dyvil.lang.Int.apply(10)
```

##`null`, the type of the `null` literal

When the compiler tries to infer the type of an expression that evaluates to `null` during compile-time (usually `null` itself), the `null` type gets inferred. For example, a variable such as

```scala
var n = null
```

gets inferred to be

```java
null n = null
```

Since the only value that is compatible with the `null` type is `null` itself, it is not possible to assign any other value to the variable `n`.

```java
n = "a" // compilation error - incompatible
```

##Primitive Types

The following primitive types are supported in Dyvil:

| Name    | Bits  | Signed | Floating-Point |
|---------|-------|--------|----------------|
| void    | 0     | -      | -              |
| boolean | 1 (8) | -      | -              |
| byte    | 8     | yes    | no             |
| short   | 16    | yes    | no             |
| char    | 16    | no     | no             |
| int     | 32    | yes    | no             |
| long    | 64    | yes    | no             |
| float   | 32    | yes    | yes            |
| double  | 64    | yes    | yes            |

Primitive Types share the same properties as primitive types in Java. However, there is one important difference: They can be used within generic type arguments, such as `List[int]`. This is only syntactic sugar though, as it will be converted to `List[Int]` at runtime, thus not eliminating the need for boxed values.

Boxed types for the primitive types can be found in the `dyvil.lang` package. They share the same name, although the first character is capitalized (`Int`, `Boolean`, etc.). The wrapper classes provide boxing and unboxing methods (`apply` and `unapply`) as well as all operator implementations (`+`, `*`, `&`, `^`, ...)

##Reference Types

Reference types are named references to existing non-generic types. They are, among generic types, the most commonly used types in Dyvil. As of Dyvil 1.0, it is not possible to qualify types names. Instead, the qualified package name has to be `import`ed before the type can be used, unless the type is implicitly imported through the [[Lang Header]].

##Generic Types

Generic Types provide a way to make operations available on different types of objects without having to redefine them. A method that gets the first element of a list of any type can be written as follows using a combination of Generic Types and Type Variable Types.

```java
static T getFirst[T](List[T] list) = list[0]
```

The generic type `List[T]` allows any `List` to be passed, be it `List[String]` or `List[int]`, and adapts the return type of the method accordingly. The type `List` can be parameterized with another type because it was defined as

```scala
interface List[T] extends Collection[T]
```

Similarly, the type `Map[K, V]` can be used with two parameters, for example as `Map[Date, Person]`.

Depending on the [[variance annotations|Variance]] of the type variables in a class declaration, Generic Types can have different subtyping relationships. For example, the tuple class `dyvil.tuple.Tuple2` is defined as

```scala
class Tuple2[+A, +B]
```

which means that the type variables `A` and `B` a both covariant. This defines the subtyping relation between parameterized Tuple2 types as follows

```
Tuple2[A, B] <: Tuple[X, Y] if A <: X and B <: Y
```

For example, for the type `Some[+A]`, a `Some[String]` is a subtype of `Some[any]`, because `String` is a subtype of `any`.

##Tuple Types

A specialization of Generic Types are Tuple Types. They represent the parameterized class `TupleX[T1, ..., TX]`, where `X` is the number of elements in the Tuple. For example, a variable

```scala
var tuple = (1, "a")
```

gets its type inferred to be `(int, String)`, which is syntactic sugar for `dyvil.tuple.Tuple2[Int, String]`. Tuple Types are [[Covariant|Variance#Covariant]], which means that `(int, String)` is a subtype of `(any, any)`, and an expression of the former type can be used where the latter type is required

```scala
(any, any) tuple2 = tuple // ok
```

##Function Types

Another specialization of Generic Types are Function Types, which represent syntactic sugar for parameterized `dyvil.function.FunctionX` types, where `X` is the number of parameters. For example, the function type `(String, int) => boolean` is syntactic sugar for `Function2[String, Int, Boolean]`. The last type argument (in this case `Boolean`) represents the return type of the function type.

As with Tuple Types and some Generic Types, Function Types are also fitted with [[variance annotations |Variance]], as shown in the declaration of `dyvil.function.Function2`.

```scala
interface Function2[-P1, -P2, +R]
```

However, the parameter types are not covariant, but [[contravariant|Variance#Contravariance]]. This inverts the subtyping relationship, and makes a `Function2[any, any, String]` as subtype of `Function2[String, String, any]`.

##Type Variable Types

Type Variable Types are simply references to [[Type Variables]]. Their subtyping behavior is defined by the bounds of the type variable, which means for a type variable

```
T <: Number
```

A type variable reference `T` only accepts types that are subtypes of `Number`. If the type variable is unbounded, type variable types accept any type.

The most important use of Type Variable Types is type inference within methods. For example, a method

```java
static List[T] listOne(T element) = [ element ]
```

adapts its return type depending on the inferred type of the type variable type.

```scala
var list = listOne("a") // list has the type 'List[String]' because 'T' was inferred to 'String'
```

##Wildcard Types

Wildcard Types are a way to allow use-site variance. For example, since the type `List[T]` is invariant on `T`, a `List[String]` cannot be used in place of a `List[Object]`. However, this problem can be avoided using wildcard types:

```java
List[String] strings = [ "a", "b", "c" ]
List[Object] objects = strings           // type error - List[String] is incompatible with List[Object]
// solution:
List[_ <: Object] objects = strings      // List of 'something that is a subtype of' Object
```

The above example shows how wildcard types can be used for covariant subtyping problems. However, it is also possible to do the same for contravariant problems:

```java
List[_ >: String] strings = objects   // List of 'something that is a supertype of' String
```

In this example, `List[Object]` is compatible with `List[_ >: String]` because `Object >: String`, i.e. `Object` is a supertype of `String`.