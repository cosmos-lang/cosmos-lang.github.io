---
layout: post
title: Declarative for-statements
---

With the latest update, we introduce a long-awaited, revolutionary feature... for-statements!

Why?
---

From the beginning, our goal was a language that can be programmed using multiple _styles_. These styles are different from the _paradigm/semantics_ used.

That is, you may program in an imperative style-- even if the code is declarative.
 
This gets us closer to our envisioned language.

First, let's introduce _pseudo-imperative programming_.

Pseudo-imperative programming
--

Cosmos is a logic programming language, yet we want to do imperative programming. Hence, we use the pseudo-imperative operator, `!`.

```
!x=x+1
```

This is akin to writing,

```
x2=x1+1
```

You'll note that we use the operator `!`. This indicates that we should read the code imperatively-- in any imperative language, `!x=x+1` increases the value of x by 1.

This is, however, shorthand for declarative code. For this reason, we do not then consider it to be actual imperative programming.

This can be seen in the following code.

```
fun p(x)
	!x=x+1
	print(x) //2
x=1 and p(x)
print(x) //1
```

We can freely alter the value that the alias _x_ refers to within a given relation or function. This lets us think imperatively and still get a declarative result.

Even though it's an imperative pattern, it's by any metric declarative, hence pseudo-imperative.

A for-statement
--

Now that this has been settled, we can make our for-statement.

```
for(x=1;x<=3;!x=x+1;)
	print(x) //1, 2, 3
```

Except for a ! operator, this looks exactly like a classical for-statement from an imperative language! We could not get any closer. This is of course, on purpose. We were not pleased with most attempts to emulate imperative programming in functional languages, as they are often much more complicated syntactically. To our knowledge, the language Mercury comes closest to what we wanted with a similar operator.

Why not just a for-each?
--

