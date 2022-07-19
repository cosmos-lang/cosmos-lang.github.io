## 1. Logic programming

Cosmos could be seen as a modern take on LP.

In fact, it currently compiles to Prolog code (it's a "transpiler" language).

In doing so, it aims to provide syntax sugar and utilities that may not have been there in "classical Prolog" as most know it.

This includes,
- Modules.
- Types and better error-checking.
- Functional programming.
- Operators such as _if_ and _not_.

Syntax
--

As a point of comparison,

```javascript
rel human(x)
    x='socrates'
	
rel mortal(x)
    human(x)
```

See Prolog code below.
```
human(socrates).

mortal(x) <-
    human(x).
```

While we lose the ability to define simple facts like `human(socrates)` in fact notation, note that complex relations remain mostly the same, i.e. it's possible to use LP-style programming.

The whitespace syntax is also useful when it comes to introducing more complex operators like _if_ and helps also avoid the dangling-comma problem. This is specially useful in LP as you may want to switch clauses.

All the while, we do aim to address many common criticisms of the language.

Such as...

The Syntax
--

This is becoming a tired point, but having modern operators and a common syntax (!=, >=, // for comments, etc.) in itself might be a plus for many programmers.

Having a modern syntax with familiar operators changes the programming experience quite a lot.

All the while, syntax choices that made sense back when Prolog was made, like distinguishing upper from lowercase variables, have not become popular.

Whether or not you consider this a worthwhile feature, it has not been adopted by programming at large. Some even consider it a point of criticism.

As a new language, we have decided to adopt a modern syntax whenever possible.

It's Modern
--

While syntax is subjective, there are also many objective upsides to being a modern language.

To this day, Prolog still uses naming like _string_concat_ for its variables. This is much less modular than _string.concat_, or at least, _string:concat_, while being inconsistent with _append_. 

This is indicative of lack of polymorphism, bad naming conventions for standard libs, modularity problems, etc.

Things like consistent naming are simple quality-of-life improvements that we take for granted in modern languages.

That aside, a modern language like Cosmos benefits from advances in,

- Scripting languages,
- Object-oriented languages,
- Functional languages,
- _Logic programming_ itself,

That may not have been there yet.

(It's actually worse! Many advances in LP have been proposed as far back as Prolog III, by the creators of Prolog, and are just now getting adopted. They're not even new at all.)

Runtime and overall error-checking
--

This is not frequently mentioned, but Prolog is _very_ prone to runtime errors. There's quite a difference to programming with more or less runtime errors and error-checking.

Too many variables
--

One can decrease the amount of explicit variables by nesting them in function notation, i.e. `x=double(double(2))`.

Pure by Default
--

As much as pure logic programming is possible in Prolog, it's not the _default_. A new programmer has to avoid numerous pitfalls and search among thousands of different predicates and libraries for the few that support pure logic programming in order to program logically.

Essentially, unless you have been programming for 10 years, you won't know where to look.

_Programming in logic_ is in fact the motto of logic programming. Prioritizing pure logic programming is compatible both with the decision of being a logic language and to being an user-friendly scripting language.

Constraints by Default
--

While this is somewhat experimental, the fact is that arithmetic operators generally have well-researched _pure counterparts_, yet... these are not the default.

The default operators use error-prone constructs. In modern days, this would be called..._not very user-friendly._

Which is terrible!

Too much impurity
--

The main complaint has always been that Prolog programmers often have to resort to non-logical operators, specially \+ and !.

These are like the _goto_ of LP. While goto in itself is a bad programming practice, it's used to implement if, while and for-statements.

It's the same here. Less error-prone abstractions are possible in modern LP.

Even if you do need to fall back from pure logic, there are better ways to do so.

## 2. Scripting languages

The syntax of Cosmos™ is based on scripting languages. In particular, modern languages like Python and particularly prototypal ones like Lua and JavaScript.

Naturally, this makes it a good choice of a language if you're a procedural programmer thinking on trying out logic--or functional, features.

Of course, we aim to have a clean syntax even by the standards of an imperative language. The syntax should also stand out by itself.

While it is inspired by scripting languages, specifically prototypal ones, some criticisms of those same languages are also addressed. 

Bad design
--

A few features of modern scripting languages are very often considered bad design[1]. Some may find this a fault.

Some of them are,

- Redundant operators, such as === and ==.
- Variables are local by default, not global.

Cosmos adopts a few design principles, and besides, it's not an imperative language, and that alone avoids many of those criticisms.

[1] A _linter_ would prohibit use of them, for example.

Local by default
--

Variables in Cosmos are local-by-default.

Often, scripting languages require you to explicitly type _local x=2_ or _var/let x=2_ to make a variable local, rather than vice versa. This may lead to errrors.

It would make a lot sense to let _x=2_ make a local variable, allowing the user to make a global only if they do specify it.

This also means programmers have to constantly write _local_ keywords, since locals are usually intended.[1]

The latter means there's no necessity to write local keywords every time. Even a _x=2_ statement still makes x a local variable.

```javascript
rel p(x)
    x = 2 //this is local
```

See also Strictness vs non-Scrictness.

[1] Another issue is that those languages will then have `var/val/let` keywords. This is _three_ different keywords that practically mean the same thing! This is quite overdoing it.


Redundant keywords
--

Languages today go particularly far in type declarations.

`var t:Integer`

Compare it to,

`Integer t`

There are at least two more keywords (`var` and `:`) in the fist. Besides, you are making the user choose between `var/val/let` when there's close to no difference between them. Three keywords for making aa local variable is quite overdoing it. For this reason, we prefer the C-style.

Strictness vs non-Scrictness
--

The above doesn't mean we want to take an extremely strictly approach, and we take a middle ground approach.

We want to make use of the fact that type inference makes typing optional. Effectively, this is a scripting language that allows simple code like _x=2_ and typing on top of that is a bonus.

This allows for the following error,

```javascript
x = 1
rel p()
    x = 2 //clashes with previous x
```

This would be an argument for more strictness, yet, this can be solved by a code convention. Why do we have a variable holding a _magic number_ in the top scope? Usually, such variables get a special naming.

```javascript
_x = 1
rel p()
    x = 2 //clashes with previous x
```

On the non-strict side,

```javascript
x = Tuple(1,x)
```

Anything that would require typing can be done by using a built-in method, i.e. you may avoid dealing with functor types by using a Tuple.

Syntax for Modules
--

Furthermore,

```
t={
	rel human(x)
		x='socrates'
		
	rel mortal(x)
		human(x)
}
```

While inserting functions/relations in a map to create a _module_ or _object_ is a common pattern in such languages, this is often not possible with such clean syntax.

That is, code outside of a module can be simply inserted as-is into the _module_ or _object_. It's then possible to switch from an Object to a non-Object style or vice versa.


## 3. Functional languages

As we have mentioned in the Getting Started section, Cosmos adopts many principles and features that are common in functional programming languages, although they apply to *relations* rather than *functions*.

This includes immutability, common patterns and even closures, which aren't native to Prolog.

Naturally, both functional and logic languages are declarative, so some similarity is no coincidence.

It's entirely possible to ignore relational programming and use a functional style.