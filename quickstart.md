---
layout: default
---
Interpreter
---
You can try out the language by opening the interpreter and making _queries_ to the language.

```
$ cosmos -i
> x=1
| x = 1
> x=1 or 2=x
| x = 1
| x = 2
```

Writing a file
---

Make a file `hello.co` with the content,

`print('hello world')`

The file can be loaded with the `-l` flag.

```
$ cosmos -l hello
'hello world'`
```

Relations
----

Instead of functions, Cosmos has relations.

They're made using the `rel` keyword.

```javascript
//note that the there is no 'return' in the definition
//instead, the parameter y is explicit
//this is typically the 'output' parameter
rel double(x, y)
    y = x*2

double(4,x) //x is 8
```

Whereas functions have one output, relations may have zero, one or more outputs. You can check this by making queries at the interpreter.

```$
cosmos -i
> x=1 or x=2 //this query has two answers (outputs)
| x = 1
| x = 2
```

If the system picks one answer and it turns out to be invalid, the system will backtrack and pick the other.

```javascript
rel p(x)
    x=1 or x=2
    
rel main()
	p(x)
	x!=1
	io.writeln(x) //2
```

Relations may adopt function syntax. This lets relations be nested.

```javascript
double(4,x) //logic syntax
x=double(4) //function syntax
print(double(3)) //this will print 6
```

Logic-wise, `double(4,x)` is read as a statement: "the double of 4 is x".

`double(4)` reads as "the double of 4".

First-class relation
---

Relations are first-class values. It's possible to define a relation within another.
```
rel p(x)
    rel temp(x)
        x = 2
    temp(x)
    
p(x) //x is 2
```
Alternatively:
```
rel p(x)
    temp = rel(x)
        x = 2
    temp(x)
```

Functors
----

Functors are composite data.
```
functor(F, Functor) //declares an object for creating functors
x = F(1, 2) //x is assigned to a functor F composed by the values 1 and 2
x = F(1, a) //uses pattern matching to match F(1, 2) against F(1, a)
print(a) //2
```
The special relation _functor_ is used to declare F as an object for making functors.

Lists are syntax sugar for the functor Cons. Here are two ways to define a list:

```
l = [1, 2]
l = Cons(1, Cons(2, Cons))
```

Relations such as _first_, _map_ and _filter_ can be used to manipulate lists.

```
l = [1,2,3]
list.first(l, head) //head is 1
list.rest(l, tail) //tail is [2, 3]
list.map(l, math.inc, l2) //l2 is [2, 3, 4]
list.map(l3, math.inc, l) //l3 is [0, 1, 2]
list.filter(l, rel(x) x!=3;, l4) //l4 is [1, 2]
```

Immutability
----

Variables are immutable. Instead of modifying a value we create a new one.

```
l2 = list.push(l, 55) //instead of modifying l, we create a new variable l2
io.writeln(l)  //[1, 2, 3]
io.writeln(l2) //[1, 2, 3, 55]
```

Cosmos adopts many principles and features that are common in functional programming languages (although the principles apply to *relations* rather than *functions*).

Types
----

Cosmos manages a balance between strictness and non-strictness. Writing the type of a variable is (almost always) optional.

```javascript
    Integer n = 7
    Real x = 5.2
    String s = 'abc'
    z = 5 //z is implied to be an Integer
    Functor l = [1, 2, 3]
    functor(F, Functor)
    Functor f = F('apple', 5)
```

The type system supports *composite types*.
```
    Functor String Number f2 = F('apple', 2)
```
*Functor String Number* is a composite type that accepts any functor whose first element is a string and second is a number.
```
    Relation Any Any p = double
```
Relations get composite types. *Relation Any Any* is a type that accepts any relation with exactly two arguments.

Tables
----

Tables (also known as maps, dictionaries, etc.) are structures that map keys to values.

```javascript
Table t = {x=1 and y=2}
table.set(t, 'a', 1, t2)

print(t) //{'x': 1, 'y': 2}
print(t2) //{'x': 1, 'y': 2, 'a': 1}
```

Making a module
---

Cosmos files are typically given the .co extension.

```js
//x.co
rel p(x)
    x=2
	
t = {
	'p' = p
}
export(t)
```
As we have mentioned, Cosmos is in part inspired by imperative scripting languages--specifically, prototypal ones. 

The principle is thus the same. The relation `p` is inserted into a table, which is then exported.

This could've been written as,

```js
//x.co
t = {
	rel p(x)
		x=2
}
export(t)
```

We then use the special relation `require`,

```
require('x', x)
x.p(2)
print(x) //2
```

Whitespace
----

The language is whitespace sensitive.
```js
rel p(x)
    x!=1
    x<5
```
This could be a single line.
```js
rel p(x) x!=1 and x<5;
```
It's possible to drop the whitespace semantics by writing the unnecessary characters, although this is not generally advisable.

Note that statements are separated by _ands_ (semicolons are only used to end the indendation).

Booleans
----

There is no boolean type. Instead, relations themselves are "booleans".

Using cases
---

`and/or` is a huge part of the language. Hence, there are many operators that are shorthand for `and/or`. One of them is `case` (alias: `cond`).


```js
case
	s = 'a'
	x = 1
case
	s = 'b'
```

This is sugar for,

```
(s = 'a' and x=1) or (s = 'b')
```

You could even use `when`, which is simply a different form of _case_.

This could be written as,

```
when(s = 'a')
	x = 1
else
	x = 'b'
```

Note that the condition is kind of redundant here.

That's why the actual if-statement and favoured conditional of the language is as follows.

Conditional
---

```js
if(s = 'a')
	x = 0
else
	x = 2
```

A conditional is equivalent to,

```
(s = 'a' and x = 0) or (not s = 'a' and x = 2)
```

Or,

```
(s = 'a' and x = 0) or (s != 'a' and x = 2)
```
 
Negation is complicated
---

Let's see an example of a more complex condition.

```js
rel main(x)
	if(p(x))
		x=1
	else
		x=2
```

The condition this time is p(x). How do we negate an arbitrary relation like p(x)? All the while keeping the code logically pure?

The operators `not/if/while` are more complicated than they seem on the surface. Still, the result should be as expected. In order to ensure it's sound, _p(x)_ may be called twice or delayed. In the worst case, `x=1` might be executed before `p(x)`.

This can always be turned off by making it a function,

```
fun main(x)
	if(p(x))
		x=1
	else
		x=2
```

When encased in a function, _if_ behaves as an imperative conditional. It will not do any _backtracking_ or _non-determinism_.

As a principle, code that uses `rel` should behave like a pure relation and code using `fun` like a regular function as in functional or procedural programming.
 
while
---

This is an example of a while-stm that writes numbers from 1 to 6.

```javascript
init x=1
while(x<6)
	print(x)//1,2,3,4,5
	next x=1+x
print(x)//6
```

Cosmos is a paradigm-neutral language. A procedural style of programming is still possible as long as the result is a pure relation or function. Procedural code is invariably self-contained and uses explicit keywords. Here _init x=1_ declares that the initial value of _x_ is 1 and _next x_ refers to the next value within the loop-_print_ of course is not pure.

Impure operators
---

The addition of function and relation modes is meant to be an improvement over Prolog's _negation-by-failure_. By comparison, standard-compliant Prolog deprecates usage of the `not` keyword at all and many logical operators are by default not pure. This makes it more-or-less difficult to try out logic programming with pure relations at all.

Though we still provide a few non-pure operators that can be used anywhere like _once_.

```
//this will only select the first answer given by p(x)
once p(x)
```
