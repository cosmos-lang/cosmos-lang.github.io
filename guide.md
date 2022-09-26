# Guide

1. Syntax
2. Introduction 
- 2B. Relations
- 2C. Operators
- 2D. Data
- 2E. Tutorial
3. Programming
- 3A. A tutorial
- 3B. Functions
- 2C. Operators
4. Optimizations

# 1. Syntax

Syntax
---

|Syntax |Output
--- | --- |
|`#str`|`size(str)`
|`t.x`|`table.get(t,x)`
|`t['x']`|`table.get(t,x)`
|`t.x:2`|`table.set(t,x,2)`
|`:f(2)`|functor

|Types | Data
--- | --- |
|`String`|`"str"`
|`Number`|`1, 2.5`
|`Relation`|`rel(x) true;`
|`Functor`|`Tuple(x)`
|`List`|`[1,'2']`

|Operators| 
--- | --- |
|`and,or`
|`if,when,choose`
|`not,once`

|Arithmetic Operators |
--- | 
|`+ - * /`
|`< > <= >= = !=`

|Conversion (casting)|
--- | 
|`str`
|`int`
|`num, real`

Lexicon
---
Syntax: a language's grammar.

# 2. Using the Language

Installation
---

Before doing anything, you may check that you've installed the language. By opening the language with the -v flag, you should see installation version number and confirm.

Open a command-line and type,

```
$ cosmos -v
Cosmos 0.16
```

If the language is installed, you'll see something akin to this.

Interpreter
---
A good way to try out a new language is by opening the interpreter, if one is available, and making statements in it. This can be done with the -i flag.

We'll assume you have already downloaded the language.

```
$ cosmos -i
> x=1
| x = 1
> x=1 or 2=x
| x = 1
| x = 2
> str='hello'
| str = 'hello'
> l=[1,2,3]
| l=[1,2,3]
```

This way, you should get a better idea of how the language works. Whenever you see a new kind of statement in this guide, you may use the interpreter to try it on.

Writing a file
---

Make a file `hello.co` with the content,

`print('hello world')`

A program that writes "hello world" on the screen is one of the simplest programs you can do. This can be done with a `print` command.

The file can be loaded with the `-l` flag.

```
$ cosmos -l hello
'hello world'`
```

### 2. From First Principles

Statements
---

A simple way to make a statement in Cosmos is to use equality, aka the `=` operator.

```
x=1
y=z
2.5=z
```

These are three kinds of statements you can make.

```
x=1
print('hello world')
io.writeln('hello world')
```

The first uses the relation of equality.

Then, the built-in `print` relation is used to write 'hello world'.

Finally, a `writeln` relation is taken from a module `io` to write 'hello world'.

Joining statements
--

```
x=1
y=2 and x=1
```

Statements can be joined together with _and_.

Statements from separate lines are implictly joined.

```
x=1
y=2
```

... is the same as ...

```
x=1 and y=2
```

Data types
--

Two basic types of data we've seen so far are _Number_ and _String_.

_Number_ includes 1, 2 and 2.5.

_String_ includes 'hello world' and "2".

Unlike numbers, strings refer to a piece of text surrounded by double or single quotation in code. 

`2` is a number but `'2'` is a string.

Comments
---

Comments are text that gets ignored by the language. They may be single-line `//` or multi-line `/* ... */`.

```javascript
//this program prints hello world
/*
	this program
	prints hello world
*/
print('hello world')
```

Arithmetics
---

Constraint Arithmetics
---

Cosmos interprets arithmetic statements as constraints. We consider this to be a step further in our exploration of logic programming as even constraint languages often have classical arithmetics as its default system. One would think it is odd for a LP language to have classical, non-logical arithmetics, as it's practically asking users to make  programs that are incorrect logic-wise.

Programs that use arithmetic are thus logically pure _by default_ in Cosmos.

```
$ cosmos -i
> x=1+y
| x = 1+y
> x>5
| x > 5
```

_What is a constraint?_

A regular language would have _x>5_ or _y+1_ simply fail. In those cases, it doesn't know the value of x or y. It wouldn't then be able to solve those equations.

Cosmos gives those the same treatment as equality; they're simply taken as true until proven wrong. Such statements are stored as _constraints_.

There are many known constraint systems. However, most would not work well as the default arithmetics. CLP(FD) is limited to integers which would mean users couldn't use floating-point numbers at all. Thus, Cosmos uses CLP for Reals[1].

However, one can use other systems by calling the host language.

[1] As far as we know, CLP for Reals goes back to Prolog III. See http://prolog-heritage.org/en/ph30.html.

_What should I worry about?_

It's possible to force a variable that may not be fully instantiated to be displayed to the user. This is done with special functions like _int_ and _str_.

This is akin to _casting_ in procedural languages.

`x = int(2+1*4/2)`

This will also force an expression that may not be an integer into one.

If the expression is not fully instantiated, an error will be given.

```
x=1+y
print(x) //1+y
print(int(x)) //this will lead to a runtime error, as y is not known
```

Non-numeric data types, such as strings, may have their own interpretation of addition. Hence, we may use addition to "add" two strings together.

```
s='hello '+'world'
print(s) //'hello '+'world'
print(str(s)) //'hello world'
print(str('hello '+x)) //error
```

It's often not necessary to cast a number as the arithmetics system will take care of that by itself. Therefore, the user should only worry about it on corner cases.

```
x=1+2
print(x) //3.0
```

_How is this different from casting in other languages?_

Casting on Cosmos will,

1. Properly instantiate a variable from an equation to an atomic value, if necessary,
2. If that isn't possible, issue an error,
3. In the case of _int_, it'll also convert the variable to an integer, even it's a floating-point number.

### 2B. Relations

What is a relation?
---

Logic concerns with statements that may be _true_ or _false_, such as,

```
x equals 2
The double of 2 is 4.
Socrates is a human.
It's raining.
```

What these statements have in common is that they each have a _relation_. This is more evident when written in logic notation,

```
x = 2
double(2, 4)
human('socrates')
rain().
```

The relationship in _double(2, 4)_ is _double_, which we defined beforehand. Naturally, this statement is true.

Out of those, equality and arithmetics do not need to be in logic notation. Generally, you write statements involving arithmetics in arithmetic notation.

As it deals with logic, statements and relations, Cosmos™ might be considered a _logic programming language_.

Logic and function notation
---

```javascript
double(4,x)
x=double(4)
```

Consider these two statements. Although the meaning is the same, one of them uses _double_ as a relation and the other uses it as a function.

Custom Statements
---

Let's codify the intuition that "the double of x is y".

```
rel double(x,y)
	y=x*2

double(2,z)
```

We've seen statements that use built-in relations like _print_ and _=_ but this is the first time we _define_ our own relation. Specifically,

1. We define a relation using the keyword `rel`.
2. We then "call" upon that same relation.

A fine rule to understand the second step is to substitute the statement for the definition.

A statement like `double(2,z)` is, by our definition, `z=2*2`, once we've substituted `x` by `2` and `y` by `z`.

In other words, the result is that z now equals 2*2.

Though _double_ is not particularly useful, relations in general can single out pieces of code allowing for later use.

As we'll see later, relations can be kept in a _module_.




Whitespace
----

Any major "structure" such as rel and if are delimited by an increase in whitespace (generally, comprised of four spaces or a single tab character).

```
rel(true)
	false
```

The code that comprises the if- and else-parts are evident through this method.
	
An error is issued if there's any inconsistency. For example, if you chose the first indent to be four spaces but the second to be three.

As long as you make a consistent rule, i.e. four spaces or one tab-only, there should be no issues.

[1] As suggested by the programming language Python™, true statements can be used as placeholders.

### 2C. Operators

and/or
---

In a logic language, these operators are more important than they may first seem. They are not only logical operators, they describe the flow of a logic language.

We've already seen them in use.

```
> x=1 and 2=y
| x = 1 and y = 2
> x=1 or 2=x
| x = 1
| x = 2
```

_Logic/declarative interpretation_

A and B: Both A and B are true.

A or B: Either A, B or both are true.

More about truth
--

As long as a valid interpretation for the statements holds, the interpreter will reply with an "answer".

It's possible there's no answer to be found, in which case the interpreter might not reply at all or give _false_ as an answer.

```
> x=1 and x=2
| false
```

The above statement is clearly a contradiction, thus untrue. The two statements can't be both true at once.

Any other answer besides _false_ is implictly a _true_ answer, even if the interpreter doesn't say so.

No matter what the interpreter outputs, it's to be taken as true until said otherwise.

```
> true
| true
> false
| false
```

The statements _true_ and _false_ both give a true and a false answer, respectively.

The Procedural interpretation
--

Cosmos is a language based on logic. Still, it runs on a computer. As such, there has to be a procedural (i.e. a machine-based) explanation on how the program runs.

We may call it the logic-procedural or simply procedural interpretation. This would be the _procedural_ explanation on how our _logic_ program is run.

_Procedural interpretation_

A and B: A and B are both evaluated, in sequence.

A or B: A is evaluated. If that fails, B is evaluated.

We might say it's a logic program that's run by a procedural "logical engine".

Let's say we have the statement `x=1 and x=2`.

A more complicated example
--

`x=1 or x=2` essentially states that x may be 1 _or_ 2. Which is to say, we don't know what the value is!

But what about `(x=1 or x=2) and x!=1`?

```javascript
rel p(x)
    x=1 or x=2
    
rel main()
	p(x)
	x!=1
	io.writeln(x) //2
```

Logic and procedural interpretations
--

Naturally, we have said that x is 1 or 2. Since we then state that x _is not_ 1, it's only possible for it to be 2. This is the logical interpretation of the program.

The program will then call io.writeln to write 2 on the screen.

1. As p(x) is called, first x=1 is evaluated.
2. However, we then evaluate x!=1. A contradiction is found.
3. _However,_ we can still go back. Our program then backtracks to p(x), and evaluates x=2.
4. This time there are no contradictions.
5. It prints succesfully.

This is a proccess that, by the way, would not exist in a truly procedural language. A procedural program has no concept of backtracking. That is, it has no _or_. It's as if only _and_ is used.

It's because this is a logic language that we must ensure our program works correctly.

Limitations
---

This brings us to the well-known limitations of LP.

1. Infinite loops

Let's consider,

```javascript
rel p(x)
    p(x)
    
p(x)
```

The program will call p(x), which will call p(x). This is an example of recursion. This is an example of an infinite loop, as the program will run forever.

The problem with this is that even correct logical problems may fall into an infinite loop.

2. Performance

The other issue is that you may need to be wary of the procedural evaluation of a program when making a program that needs good performance. The logic aspect of the language may trick into thinking you don't need to pay attention to the procedural. However, the order in which the statements are evaluated matters in a real program.

A Counterpoint
---

A possible counterpoint is that-- every language has the same problem, that is, they too can fall into infinite loops.

Couple that with the fact this occurs when you're doing recursion. Generally, if your program relies on a relation calling itself it's pretty obvious that it's doing so, and you have a hint that you should be looking out for such things.

The second point is a result of combining a query solver with a programming language. If you simply want the solver to answer a query, does it matter if it takes a few seconds (or less) longer?

The programmer then wants to instead use it as a blazing fast programming language, while at the same time expecting it to be fast without doing any work on optimizing it- which is not how it works in any language. 

Even if it's not ideal, knowing how the program works is often necessary to optimize it in any language.

### 2C. Extra Operators

Operators
----

Adding to our repertoire, we have _if_ and _not_.

Logically speaking, this lets us represents all kinds of statements in the form,

`If X, then Y.`

`not X.`

Which are common in logic and show up in practical programming.

```
If it's raining, then someone will bring an umbrella.
If someone is a human, they're mortal. (aka All humans are mortals)
It's not raining.
```

_if_
--

```
if(true)
	print('condition is true')
else
	print('condition is not true')
```

We may again open the interpreter to try if-statements.

```
$ cosmos -i
> if(x!=1) x=2;
| x=2
> if(x!=1) x=2 or x=1;
| x=2
| x=1
> if(x!=1) x=2;
| x=2
```

The body of the if-stm will be evaluated when the condition, e.g. x=1, is true.

```
> if(false) x=2 else x=1;
| x=1
> if(x=1) x=1 else x=0;
| x=1
| x=0
```

It's possible for an if-statement to have an else-clause. If the condition is true, the if-part holds, otherwise the else-part holds.

In the latter example, the interpreter tried out both possibilities and gave two answers.

_elseif_
--

```
if(x=1)
	y=2
elseif(x=1)
	y=2
else
	true
```

Naturally, this is just a way to write,

_Logical interpretation_

You may think of an if-statement as equivalent to,

`if(A) B else C; <==> (A and B) or (not A and C)` 

An if-statement without else is,

`if(A) B; <==> (not A) or B`

Though this may not be its exact implementation.

_when_
--

It's easy to imagine a situation where negating the condition is unnecessary.

```
when(l=[])
	print('list empty')
else
	l=[h|t]
	print('list gotten')
```

An if-statement would add a _not_ for safe measure, resulting in `l!=[] and l=[h|t]`. The second statement already covers the former; a programmer may fine-tune such a statement by switching to the the _when_ conditional.

_Logical interpretation_

The _when_ operator is simply syntax sugar for _and/or_,

when(A) B else C <==> (A and B) or (C) 

It's similar to _case_. In fact, it's a different way of writing _case_ statements.

As you see, this is a rather barebones conditional.

As the _else_ is redundant it's simply a _case_ with a conditional syntax. However, it's easily switchable with other conditionals due to this syntax. A _when_ can easily be changed to _if_ and vice versa.

When the programmer wants to write _case_ statements or use conditionals with a customized negation, they may use _when_.

Of course, despite the different semantics both _if_ and _when_ are pure code.

_not_
--

```
> not x=2
| x!=2
> not 5<1
| x=1
| x=0
> not x<=2
| x>2
```

_not_ simply negates a statement.

_Logical interpretation_

The negation of A is false when A holds, and true when A doesn't. 

Complex Conditionals
--

It's recommended keeping the conditions for an _if_ or _not_ to simple statements.

Simple statements like equality or inequalities, i.e. =, !=, >, etc. are more tried-and-true. They've been more extensively tested.

It's easy to see that _not x=1_ is the same as _x=1_. Similarly, _not x>5_ is just _x<=5_.

By contrast, negating a generic statement like _p(x)_ or _q(x,y)_ is more complicated. Cosmos' current approach is to delay the evaluation until all its arguments are instantiated[1].

Nonetheless, it's valid logic code. 

```javascript
rel p(x)
	x=2
    
not p(x) //x is not 2
x=1
```

Negating _p(x)_ means keeping the call to _p_ in hold until _x_ is instantiated, i.e. _x=1_.

[1] As far as we know, this is the best way to safely negate a relation assuming we don't have information on how the relation is coded.

_Procedural interpretation_

The negation of A is obtained by delaying the evaluation of A until its parameters are instantiated. When it's done, the result will be false when A holds, and true when A doesn't. 

Limitations
--

```javascript
rel p(x)
	not q(x)
    p(x)

p(x)
```

As stated previously, LP is not above infinite loops.

When running this example, _q(x)_ is skipped entirely, leading straight to _p(x)_. This will create an infinite loop.

Alternatives
--

Our current implementation of negation plays it safe and may delay a statement until it can be sure it can be evaluated; if a statement is too complex for our not or if-statement, it’ll be delayed.

We fully expected someone very acquainted with logic programming may prefer to implement their own negation. If a more specific implementation of conditional/negation is required, this may be done using the operator _when_. 

```javascript
when(x=2)
	true
else
	x!=2
```

Finally, many examples of logic programming (such as the one given previously in the tutorial) do not need negation at all. 

```javascript
rel likes(x,y)
	when(x='alice')
		y='cake'
	else
		x='abbe'
		y='pastry'
```

_when_ is simply a shortcut to 'and/or'. You are thus free to fine-tune your own negation or not at all.

Finally, you may use a _function_.

A function is constrained in many ways; it only needs to run once. Programmers writing deterministic programs may only need functions, and a function is more straightforward in those situations.

```javascript
fun p(x)
	if(not q(x))//error
		p(x)

p(x)
```

A function will simply display an error if it can't execute the condition. This is much like what a procedural or functional language would do.

When using a relation, our main concern is that the operators behave in a _purely relational_ way. As we're using a function, a way befit of a _pure function_ is enough.

Pure functions are way simpler than pure relations. They don't return multiple answers, and don't work without non-instantiated arguments.

Logic-Procedural (II)
--

Our main requirements _if_ (and _not_) are that,

- It's a logically sound conditional.
- If it can't do that, an error is given.

The reason for this is that we want to allow for different optimizations and ways to implement a logical conditional/negation to be tried.

For us, being able to use a sound conditional is already an improvement. Prolog famously implemented negation in an unsound way (that also gave no warnings whatsoever).This 

This has highly limited experimentation with logic programming, as two operators were rendered mostly unusable.

Functions
--

A relation can be turned into a function by changing the `rel` to a `fun` keyword.

```
fun q(x,y)
	if(p(x))
		y=2
	else
		y=1
```

As functions have simple requirements when compared to full relations, an _if_ or _when_ will accept any conditions when inside a function[1].

Because a function is only meant to run once, there is no need to support backtracking or any other logical mechanisms.

This may mean we're abandoning relational programming (LP) for a moment, though this is restricted to _q_.

We'll explain this further in a later section.

[1] The semantics of _if_ or _when_ will be turned into that of a _commited-choice_ conditional, which we call the _choose_ operator.


List of Conditionals (Summary)
--

if: guaranteed to be logically sound, gives error if the condition is too complex.
when: simple conversion to and/or. Even if it fulfills the condition and goes to if-code, it may still backtrack to else-code. Works for any condition.
choose: simply checks if the condition is true, then chooses if or else-code. It'll not backtrack, but then this may not be logically sound.

We recommend sticking to _if_ when possible.

_if_ works best with simple conditions, i.e. simple inequalities such as != or >=.

<!--If this is unreasonable, a simple solution is to fall back into functions, which we'll explain in a later section.-->

A Conditional in Formal Logic
--

This is just trivia, but it may be of interest to some that the actual conditional _A->B_ in formal logic does not have an _else_.

It's simply something adopted from procedural programming where we often specify what to do if a condition is not true. This has often been adopted by LP aswell.[1] 

`If it's raining, then I will fly.`

An odd thing about the formal conditional is that it holds true when the condition is false. As we said before, `if(A) B; <==> (not A) or B`. 

This is actually rather arbitrary! The implication is that if we confirm that it did not rain, then this odd implication is true.

Perhaps we'd rather say: "you would not fly anyway!"

That would maybe render the implication false.

What about an implication that is always false when the condition is false? This would be arbitrary aswell.

Though this may be a moot point, we may conclude the formal implication is not the same as the implication we use in natural language.

There is no justification given for any of this.[2] It was simply deemed useful to take a conditional as true when we can't say otherwise.

It's useful in our programs to say,

`If the switch is set, our program will beep.`

And, if the condition doesn't hold, simply go on with our program. We're going by the assumption that our machinery is correct.

[1] See reif or `(->;)`.
[2] One may consult the _Principia Mathematica_ for a definition and explanation of the logical implication and see that, once again, it's an arbitrary definition.

Whitespace
----

It's about time we explained our use of whitespace and indendation.

Any major "structure" such as rel and if are delimited by an increase in whitespace (generally, comprised of four spaces or a single tab character).

```
if(true)
	false
else
	false
```

The code that comprises the if- and else-parts are evident through this method.
	
An error is issued if there's any inconsistency. For example, if you chose the first indent to be four spaces but the second to be three.

As long as you make a consistent rule, i.e. four spaces or one tab-only, there should be no issues.

Syntax-wise, whitespace only adds _ands_ to the end of lines (unless a keyword like _else_ or _case_ pops up) and ends any unindent with a _semicolon_.

As such, the semantics of whitespace are very easy to understand.

Coming from a procedural language, it may seem odd that a semicolon is used to end a structure.

Still, this is in line with the syntax of most LP language.

### 2D. Data

Functors
----

We start with a declaration.

```
functor(F, Functor)
```

By using the special relation _functor_, we declare that _F_ is a functor, or rather, it's what will be used to make functors. We can now make functors with the name/label _F_.

```
F(1, 2) = F(1, a)
print(a) //2
```

Functors are a kind of composite data. They are what some languages call a _tuple_.

If 1 or 'hello' is a single value, F(1,'hello') is a value made from combining both. 

We made two functors. Since they are equal to each other, we can also conclude that its values are. Hence, `a=2`.

A Practical Example
---

Let's say we want to represent a person in our program. We could just make a functor `Person`.

```
functor(Person, Functor)
```

We can now make our first person.

```
bob = Person('bob', 23)
```

We have made the convention that the first two fields of `Person` stand for name and age, though if needed we could have included more fields. This allows us to make programs about one or more persons!

This is not the only way we could represent a person, of course. Cosmos™ has _objects_ aswell, which are very similar in that sense! We'll cover them later.

Tuple
---

If we simply to group things together, any functor is enough. We may use a _F_ or _Tuple_ functor for this.

```
> Tuple(x,1) = Tuple('x', y)
| x='x' and y=1
```

Lists
---

A list is another kind of composite data. Let's say we want a list of things. This can easily be done with the syntax,

```
l = [1, 2, 3]
```

We've made a list with the values 1, 2 and 3.

There are operations we can make on lists. We can add, subtract or search for elements within it. These can be found in module list.

```
l2 = list.push(l, 55)
io.writeln(l)  //[1, 2, 3]
io.writeln(l2) //[1, 2, 3, 55]
```

If we _push_ value 55 into l, we'll get a new list l2 with elements.

```
l = [1,2,3]
list.first(l, head) //head is 1
list.rest(l, tail) //tail is [2, 3]
l=[head|tail]
```

A common operation is to get the _first_ element in a list, or the _rest_- the remaining, which itself is a new list. These are sometimes called the head and tail of a list.

This is a common pattern in declarative programming, and as such there's even a special syntax for it.

l=[head|tail]

The term [x|y] is very different from [x,y]- the latter is a list with two elements. The former is any list.

Lists as Functors
---

Lists are often implemented in terms of the functor Cons. These lists are identical:

```
l = [1, 2]
l = Cons(1, Cons(2, Cons))
```

### 2E. Modes

Functions [Incomplete]
--

_"A function is a less general kind of relation." - The Cosmos Programming Language_

While a relation may give multiple answers-- or no answer at all (in which case the statement is taken to be _false_), a function is guaranteed to only give one.[1]

[1] A function here is meant to mimic a typical _programming function_ that you often see in procedural or functional languages. It's not necessarily a mathematical function. For example, it may accept more than one input.

A Factorial Function
--

There's no clear rule on what should or shouldn't be a function.

We'll take _factorial_ as a good case.

- It's often a function in mathematics.
- It may run multiple times. As such, it often benefits from whatever optimizations we may give it.
- You don't usually need anything more than simply getting its result.

```
fun fact(x,y)
	if(x=0)
		y=1
	else
		y=x*fact(num(x-1))
```

Mixing functions with relations
--

The language tries its best to accomodate both types of programming. When using a relation, _if_ is a logical conditional and will behave soundly to the best of the language's ability. When using a function, _if_ is allowed to use lower-level predicates, as there are way less requirements that a function needs to meet.

fact(2,y)

Even if "low-level LP" operators are present, they're subsumed by the use of functions. Although this may perhaps be considered leaving the paradigm, it's much cleaner than using the aforementioned operators. For what it's worth, functions themselves frequently appear in formal logic. This also opens up the possibility of using Cosmos as a functional language.

At least, the language is not pretending something is a logical predicate when it isn't. When you do use a logic predicate--that is, a rel, the language will take it that you're programming in the logic paradigm, so as to make pure logic programming possible and easy.

It's purposefully easy to switch between those and compare their behaviour, as one only has to change the appropriate keyword.  

A Main Function
--

## 3. Programming

### 3A. A "Prolog" tutorial

A common way to introduce logical languages is by emphasizing its relation to logic. Although it's not very practical, it's as good as any tutorial or introduction nonetheless.

Let's make it clear that,

- A program is a set of relations.
- These relations are then _queried_.

```
rel human(x)
	x='socrates' or
	x='plato'
	
rel mortal(x)
	human(x)
```

This is easily translated to formal or informal logic,

```
Socrates is human.
Plato is human.
	
If x is human, then x is mortal. (aka All humans are mortals).
```

Or...

```
human('socrates')
human('plato')
mortal(x) <- human(x)
```

Although we converted our definition of _mortal_ to a conditional, it's a conditional going the opposite way. The body of our relation, `human(x)`, implies `mortal(x)`.

Querying
----

We can then make a query to the interpreter,

```
> human(x)
| x='socrates'
| x='plato'
> human('socrates')
| true
> mortal('socrates')
| true
> human('bill')
| false
```

Naturally, no 'bill' exists in our program. We have not included Bill in our definition, so that either Bill is irrelevant to our program, not human, or our definition is flawed.

The query _human(x)_ is akin to asking "Who is human?" Because x is a free variable in _human(x)_, Cosmos™ will try to find valid matches-- what is a possible value for x--in other words, who is human in our program. 

A peculiarity
----

When we define a relation, it's a complete definition.

When we defined `human(x)`, we stated that a human really is either socrates or plato.

As far as our program is concerned, these are the only humans out there. 

We chose to use String to represent our humans.

The string 'socrates' is of course not the same as the living Socrates.

Possible worlds
----

Logic is a tool for reasoning about both real, hypothetical or fictional worlds. Being real is not necessary. We can reason about possibilities aswell.

We dare say Cosmos™ is a good way to try reasoning with _possible worlds_, a relatively new formalism in logic.

```
t={
	rel human(x)
		x='socrates'
		
	rel mortal(x)
		human(x)
}

t2={
	rel human(x)
		x='alice'
		
	rel immortal(x)
		human(x)
}
```

We've made a different possible world _t2_ where Alice resides as an immortal. Such high-level theorizing is in the realm of possibility for the Cosmos™ programming language.

```
> t.human(x)
| x='socrates'
> t2.human(x)
| x='alice'
```

Using _case_ or _when_
--

As explained before, using _case_ and _when_ is a good way to avoid writing a lot of and/or statements and make our definitions concise.

This was not necessary for `human(x)`, but it surely is for `likes(x)`.

```javascript
rel likes(x,y)
	when(x='alice')
		y='cake'
	else
		x='abbe'
		y='pastry'
```

We can now easily ask, "what does Alice like?"

```
> likes('alice',x)
| x='cake'
```

Negation
--

A typical tutorial of logic programming would typically end there, as the first version of the Prolog programming language did not at all soundly implement _not_ or _if_ statements.

Programming with anything more than _and/or_ as the only logical mechanism is thus not well-known by the programming community in general.

One can easily introduce negation to this scheme. However...

```
> not likes('alice','cake')
| false
> not likes('alice','pastry')
| true
> not likes('alice',x)
| not likes('alice',x)
```

As with positive statements, there are limitations. The _not_ operator is too general, as it is required to work with any statement, and will give a redundant answer to the last query. Internally, _not_ waits until all arguments are instantiated, and doesn't do anything otherwise.

As such, _Alice does not like x_ is considered a valid answer to _What does Alice not like?_.

This is, however, not that different from answering _x=2_ with _x=2_. A statement is true until proven false, and false until proven true. Such things are considered sound logic programming.

A programmer who knows the definition of _likes_ can easily implement their own version of _not_likes_ for a more precise answer.

```
rel not_likes(x,y)
	case
		x='alice'
		y='pastry'
	case
		x='abbe'
		y='cake'

> not_likes('alice','cake')
| false
> not_likes('alice','pastry')
| true
> not_likes('alice',x)
| x='pastry'
```

The will give a more precise answer to the last query. Unfortunately, this still fails as a definition if we introduce unknown elements. Like with the definition of _likes_, the definition of _not_likes_ has the assumption that we've named all objects of discourse. 

A statement `not_likes('alice','other-thing')` will be false, as there's no _unknown_ value, and likewise `likes('alice','other-thing')` will be false aswell. The negation of a statement is not supposed to hold the same truth value as the statement itself.

It's not in the domain of the language to address all these issues. Cosmos is still a Prolog-offshoot and is as concerned about being a programming language as it is about being a pure logic solver, though we do want to allow for pure logic programming-- the Prolog basis remains.

Conditional
--


Constructive Negation
--

It's recommended keeping the conditions for an _if_ or _not_ to simple statements and inequalities, i.e. =, !=, >, etc. rather than more general goals in relational programming, generally speaking.

The key issue is that full-on negation with the _not_ operator may not be what you want in those cases.

```
> not likes('alice',x)
| not likes('alice',x)
```

The operator _not_ waits until variables are fully instantiated before giving an answer, which may not be the behavior wanted in this case. We'll illustrate this by making a _non_ operator.

In this case, we may perhaps want to manually build our relation.

```
rel not_likes(x,y)
	case
		x='alice'
		y='pastry'
	case
		x='abbe'
		y='cake'

> not_likes('alice','cake')
| false
> not_likes('alice','pastry')
| true
> not_likes('alice',x)
| x='pastry'
```

Just like Prolog, our focus is divided between logic and a more general-purpose kind of programming. In fact, the existence of function declarations should make it clear we're rather _more_ concerned about general-purpose programming, although we also improve upon the language's Prolog basis[1].

The addition of constructive negation still involves quite a tradeoff and isn't part of our general schema.

We should perhaps make a distinction between _not_ and _non_.

```
Some x is human.
Some x is not human.
All x are not human.
```

`not human(x)` is an example of the last statement, while `non_human(x)` is the second. `human(x)` is an example of the first statement.

`non_human(x)` is actually a subcontrary to `human(x)` and not a contradictory statement, as `not human(x)` is, if we take the square of opposition[2] into account. Such statements can be both false.

[1] Hence, there's also a focus on building relations that are logically pure and constraints, which is not really an addition but generally not well-known as a part of logic programming.
[2] https://en.wikipedia.org/wiki/Square_of_opposition.

Making a _non_ relation
--



```
rel non(set,p,x)
	x in set
	p(x)
	
non_human(x)
	non(logic.setOf(person,x)+{'a dog'},human,x)
> non_human(x)
| x='a dog'
```

For a relation with two variables,

```javascript
rel non_likes(x,y)
	human(x)
	non({'cake','pastry'},likes,x)

> non_likes('alice',x)
| x='pastry'
```

We may interpret non_likes as the intuition "there is a human x and x non-likes y".

This could of course be defined manually,

```
rel non_likes(x,y)
	case
		x='alice'
		y='pastry'
	case
		x='abbe'
		y='cake'

> non_likes('alice','cake')
| false
> non_likes('alice','pastry')
| true
> non_likes('alice',x)
| x='pastry'
```

In both cases, it's important to specify the universe of discourse. When talking about who dislikes what, we may specify that the realm of x is humans and y is things; then, we can make a relation for "human x doesn't like thing y".

_when_ vs _if_
--

Limitations
--

```javascript
rel p(x)
	not q(x)
    p(x)

p(x)
```

As stated previously, LP is not above infinite loops.

When running this example, _q(x)_ is skipped entirely, leading straight to _p(x)_. This will create an infinite loop.


Pure Logic Programming
--

Most important for our language is the notion of a pure logic program.

Logic programs allow us to effectively write logical statements and have the language work them out correctly.

Writing pure relations
---

- Any relation made of pure relations and operators is pure.
- =, and, or are pure.
- not, if and regular arithmetic are pure.

Knowing you have written a pure relation is quite simple. Both _human_ and _likes_ are pure because we have only used pure operators-- mainly, and/or and =.

_mortal_ is pure because it calls _human_ and nothing else. _human_ is pure, therefore _mortal_ is pure.

### 3B. Pure Functional Programming

Functions [Incomplete]
--

_"A function is a less general kind of relation." - The Cosmos Programming Language_

In Cosmos, we consider a function to be a more constrained type of relation.

It's for this reason that we have functions. A relation has a much broader behavior. A programmer who is not ready to tackle all the possible behavior of a relation, may prefer to start off with a function.

Using functions then is a matter of simple restraint. A programmer simply has to keep in mind what it is.

(1) _A function receives an input and produces output._

- A function has one or more input parameters and a single output parameter, conventionally the last, typically.

In factorial(2,y) and double(4,x), the input given is 2 and 4 while the output is y and x.

(2) _A function generates one output._

- The function mode (or fun keyword) ensures this.

While a relation may give multiple answers-- or no answer at all (in which case the statement is taken to be _false_), a function is guaranteed to only give one.

In summary, if you only want a relation to run once, you may consider turning it into a function--let's say your usecase is simply computing the result of a factorial.

You want _fact(2)_ to give you the appropriate result. This can easily be done by a function.

A Factorial Function
--

```
fun fact(x,y)
	if(x=0)
		y=1
	else
		y=x*fact(x-1)
```

A programmer making a function should use it _as a function_. When making a _fact_ function, we then decide that x should be the input and y the output. This is where most non-logical languages would have a _return_ statement.

When calling fact(2,y), a function will correctly receive 2 as input and work out y--the output or "return" value. It's even possible to try the reverse.

As it's still a relational language, fact(x,2) will also work-- that is, computing the "reverse factorial". Two functions by the price of one.

However, fact(x,y) is nonsense. This can only be interpreted as a statement, one that may yield multiple answers. The function mode is only made to support functional behavior, and will not handle this.[1] 

At this point, one should switch to relations. This can be done by changing fun to rel. Fortunately, _fact_ still works well as a relation.

This is more in-tune with the kind of programming shown in section 3A.

[1] This is not completely enforced by the Cosmos™ compiler, as of yet. As such, we ask to have some caution when using it.

Conclusion
--

One can work a functional program by simply determining which variable is the input and which is the output. In x=fact(2), 2 is an input and the answer returned is x.

Knowing this, one might retrace the steps.

- 2 is compared to 0. That fails, hence we go to the else-part.
- By substitution, the output is y=2*fact(2-1).
- _fact_ is called again, etc.

Pure Functional Programming
--

A function may not be pure in the logical sense-- however, it may be pure in the functional sense. 

You'll often hear about purity in functional languages, which have no relations. That refers to functional purity.

A function is not pure when it does anything un-function-like, i.e. anything that is not receiving and returning values.

```
fun write(x,y)
	if(x=0)
		y=1
		print(x)
	else
		y=2
```


### 3C. Paradigms

Typically, programming is divided into four main paradigms,

- Procedural (imperative)
- Functional
- Logic
-- Logic-procedural (?!)
- Object-oriented

Although this classification is increasingly dated, it's still used (and somewhat useful) to this day.

Styles
---

Cosmos™ is made to support a variety of styles and paradigms.

It may be useful to distinguish between a style and the paradigm used. The user may,

- Use function syntax, despite them being relations.
- Use relational syntax, despite using functions.

This is where the distinction between paradigms start to get a little blurry. Some may call Cosmos a multi-paradigm language.

Let's take the code,

```
rel double(x,y)
	y=x*2
	
x=double(1)
```

We're free to use _double_ in function syntax, or think of _double_ as a function, even if it's a relation. 

```
fun double(x,y)
	y=x*2
	
double(1,x)
```

We've implemented _double_ as a function, but used logical syntax.

Thus, we've used a functional style in relational (logic) code and a logic style in functional code.

Similarly, one can combine paradigms as they see fit- using a function inside a relation, for example.


### 4B. Optimizations

_if_
----

Because it's the language's main conditional, any number of optimizations may be applied to it as long as it keeps its properties as a conditional (while the operator _when_ is kept for fine-tuning; if you want a minimal conditional to which you can apply your own optimizations). 

Currently, 
- Any condition is negated.

_when_ and _choose_
----

_when_ is a sound but more barebones conditional. Implementing a pure factorial relation in _when_ makes for a good case study.

_when_ and _choose_
----

_when_ is a sound but more barebones conditional. Implementing a pure factorial relation in _when_ makes for a good case study.

_when_ is a pure conditional. Still, since it requires you to manually negate the condition (which is redundant otherwise) and may not provide future optimizations, unless you implement them yourself, it's less preferred and not the default go-to for conditionals.

Remember that relations may _backtrack_ or yield more than one solution. Even if a factorial relation succeeds the first time, an ill-defined program may cause on the second solution. 

Let's compare this to,

rel fact(x,y)
	when(x=0)
		y=1
	else
		y=x*fact(num(x-1))

... or ...

	(x=0 and y=1) or (y=x*fact(num(x-1)))
		
While fact(1,x) would still work, it would for the first solution alone. Remember that relations may _backtrack_ or yield more than one solution. 

This would suffice were it a regular imperative or functional definition of factorial, since those are meant to run only once and never backtrack.

However, this is not so for a logical language and different reasoning is needed. If it ever tries to find a second solution, it will procceed to the second clause. The reader is invited to keep this in mind and accompany the execution of fact(1,x).

rel fact2(x,y)
	when(x=0)
		y=1
	else
		x>0
		y=x*fact2(num(x-1))

As you see, we have,
- Manually negated x=0, by typing x>0.

The program now works soundly, even if it's not perfect! It still creates places to backtrack or _choice points_. This consumes memory, moreso if we call _when_ a lot of times. But at least these are eliminated upon hitting x>0.

==

What then if we simply removed backtracking?

_choose_ is a non-logical conditional that doesn't backtrack.

As such, it's fit for code with side-effects. A simple prompt, for example.

rel prompt()
	print('type a number')
	io.write('> ')
	io.read(x)
	choose(x='5')
		print('You typed 5!')
	else
		print('You didn't type 5!?')
	prompt()
	
Such code is non-logical in the first place- and has no need for backtracking.

The safest option is still to rely on _if_. It should never be unsafe to use _if_. For cases it can't be used, you'll invariably be given a warning or error at least. However, _choose_ and _when_ are available if you're aware of the limitations.

_TCO_ (Tail-Call Optimization)
----
