## A Prolog Transpiler

Cosmos is an authentic, modern logic programming language that compiles to Prolog code.

By acting as a transpiler, Cosmos aims to provide many amenities to "raw" Prolog.

It should be noted that _Cosmos is its own language_. Knowledge of Prolog is not a requirement to use Cosmos at all, unless it's for low-level programming.

Does Prolog benefit from a transpiler? (Definitely.)
--

Cosmos provides plenty of syntax sugar and utilities that may not have been there in "classical Prolog" as most know it.

This includes,
- A modern syntax with conventional operators (!= for inequality, // for comments).
- Syntax sugar.
- Consistent naming.
- Modularity (modules, objects).
- Types and better error-checking.
- Functional programming.
- Operators such as _if_ and _not_.
- A better standard library.

Is Prolog Pure?
--

As much as pure logic programming is possible in Prolog, it's not the _default_. 

A new programmer has to avoid numerous pitfalls and search among thousands of different predicates and libraries for the few that support pure logic programming in order to program logically.

It's technically possible, but a careful choice of libraries have to be made beforehand.

In Cosmos, this choice is made for you. A simple construct can be compiled to use any available modern advances in LP (Logic Programming)[1]. Cosmos code is pure unless the user picks an explicitly impure construct.

_Programming in logic_ is in fact the motto of logic programming. Prioritizing pure logic programming is natural and compatible both with the decision of being a logic language and to being an user-friendly scripting language.

[1] Such as reif, clp, delaying goals as in Prolog II or NU-Prolog, etc.

Runtime and overall error-checking
--

This is not frequently mentioned, but Prolog is _very_ prone to runtime errors. There's quite a difference to programming with more or less runtime errors and error-checking.

Syntax sugar
--

Some syntax sugar can be useful aswell.

For example, function notation can decrease the amount of explicit variables, i.e. `x=double(double(2))`.

This would otherwise be,

```javascript
double(2,y_)
double(y_,x)
```

Falling back
--

If one needs to fall back from relational programming, it's possible to do so by using _functions_.

When doing so, one avoids dealing with low-level operators like \+ and !. These are widely considered the _goto_ of LP. This effectively lets one use Cosmos as a functional language.

This solves what some consider the two main issues with classical LP (i.e. Prolog). Not only is it easy to use Cosmos as an actual logical language, it's also possible to fall back when necessary.

Scripting languages
--

The syntax of Cosmos™ is based on scripting languages. In particular, modern languages like Python and particularly prototypal ones like Lua and JavaScript.

At the same time, we try to avoid common criticisms of those languages.

In particular, we avoid having redundant operators and variables are local by default, not global.

There's also quite a support for prototypal-mixed-with-logic syntax,

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

A note on syntax
--

It goes without saying that Prolog is an old language. As an old language, certain design choices may be seen as unconventional, if only because these choices weren't widely adopted.

For example, the identifier `foo` is not a valid variable name because it's lowercase. I'm sure LP enthusiasts know this. Certainly, they should also know this is unconventional in the context of modern languages and somewhat unique.

Regardless of whether this makes sense or not, we went for a more conventional approach. `foo` is a valid variable name. We take care to specify which decisions are based on familiarity (conventional design choices). Regardless, a better focus on pure LP are simply more desirable in general.

What about performance? Is it good for my application?
--

The performance of a transpiler language depends on (1) the target language's performance, and (2) how it's compiled.

The compiler relies a lot on meta-predicates to support closures. Using features such as objects will also have the predictable performance cost of using objects.

Neither Cosmos nor the target language are system languages. It's not the focus of the language.

Note however that we don't know what your application is. Please determine yourself whether this is good enough for your application.

What about a more direct C compiler?
--

A C compiler was planned at one point.

However, using a host language suffices for our goals. Even without its own compiler, Cosmos™ can already be used as,

- A simple language for scripting.
- A way to try functional or logic programming with a procedural syntax.
- An academic language...
- and more.

If you think it deserves its own implementation, please send code or support the language.