# Kotlin 



### Python-Kotlin  dictionary

| Python                               | Kotlin                                                |
| ------------------------------------ | ----------------------------------------------------- |
| *Def*                                | *Fun*                                                 |
| *Method*                             | *Member function*                                     |
| *self*                               | *This*                                                |
| *Lambda*                             | *Lambda*                                              |
| *Zip*                                | *Zip*                                                 |
| *Dict*                               | *Map*                                                 |
| *Map*                                | *Map*                                                 |
| *Filter*                             | *Filter*                                              |
| *True*                               | *true*                                                |
| *False*                              | *false*                                               |
| *int*                                | *Int*                                                 |
| *float*                              | *Double*                                              |
| *bool*                               | *Boolean*                                             |
| `print("")`                          | `println("")`                                         |
| `['a','b','c']`                      | `listOf('a','b','c')`                                 |
| `int("3")`                           | `"3".toInt()`                                         |
| `float("3")`                         | `"3".toDouble()`                                      |
| `for i,x in enumerate(alist):`       | `for ((i,x) in aList.withindex()) {}`                 |
| `'-'.join(alist)`                    | `aList.joinToString(separator="-")`                   |
| `lambda x, y: x+y`                   | `{x:Int, y:Int -> x+y}`                               |
| `lambda x: 2*x`                      | `{x:Int -> 2*x} // or even {2*it}`                    |
| `my_fun = lambda x, y: x+y`          | `val my_fun: (Int,Int)->Int = {x,y-> x+y}`            |
| `a if a is not None else b`          | `a ?: b`                                              |
| `s.foo() if s is not None else None` | `s?.foo() // if(s!=null) s.foo() else null`           |
| `s.foo() if s is not None else "x"`  | `s?.foo() ?: "x" //s.foo() if s is not None else "x"` |



### Member references (bound and unbound references)

We can store a function in a variable, creating what is called an **"unbound" reference:**

```kotlin
// let's define a function
fun myFunction(i: Int): Boolean = { i%2 == 0 }

// can assign a function but using a function reference
val f: (Int, Int) -> Double = ::myFunction 

// can assign a lambda directly without function reference
val f = {i: Int -> myFunction(i)} 

// can refer to the function anywhere
myList.filter{::myFunction}
```

We can also store a member function in a variable, creating what is called a **"bound" reference**:

```kotlin
// this is an instance of a class
val alice = Person("Alice", 39)

// this is the bound reference
val f: (Int) -> Boolean = alice::isOlder

// let's use the bound reference
f(21)
```





```kotlin
a.takeIf{predicate} // if (lambda_function) a else null
a.takeUnless{lambda_function} // if (!predicate) a else null

repeat(10){code_block} //for (i in 0..10){code_block}

run

a?.let{code_block} // if (a != null) {code_block}
```



## Inline functions

`inline fun` is a way to improve performance by simply replaces the code with the function block rather than calling the function

run, repeat, let, takeIf, takeUnless, withLock, use are all inline fun. No performance overhead. 

Warning: use with care. Only small functions must be inlined. Usually in common applications they are not needed

## Sequences

Sequences are exactly like collections, but do **lazy evaluation** (as opposed to eager evaluation). When you use normal collection and you do for example `aList.map{...}.filter{...}` a new collection is generated at each call of map, filter, etc. (so in this case we generate 3 collections: aList, the result of aList.map{} and the result of aList.map{}.filter{}). While if you use a sequence and you apply those operations, it will do the computation only in the end and you do not generate any intermediate result, having performance gain.

To convert from list to sequence, just use the `asSequence()` operator: `aList.asSequence().map{...}.filter{...}`

A sequence can also be defined from scratch using `generateSequence` or  `yield` (more advanced topic, maybe irrelevant). 

## Lambda with receiver

A *Lambda with receiver* is simply a lambda with implicit `this`. They are also called "extension lambdas" because they are the analogue of extension functions, but for lambda's.

### Some functions using lambda with receiver

- `with`: Is a regular function call which takes a variable and a lambda with receiver and calls the lambda on the variable.
- `run`
- `let` 
- `apply` 
- `also`



## Types

Kotlin types vs java types (skip). Prefer Lists over Array.

**Unit vs Nothing**: `Unit` means "the function does not return anything" (like `void` in java). `Nothing` means "the function never returns (never completes)". Examples of functions returning `Nothing` are functions always throwing exception (e.g. a "fail" function) or the TODO function (which also throws an exception). Also when you just write `return` the returned value is actually `Nothing`. If you don't write return (e.g. you just print), then the returned type is `Unit`.

Any means multiple type. For example with an `if` you can return an integer or a Nothing, then the returned variabile is Any.