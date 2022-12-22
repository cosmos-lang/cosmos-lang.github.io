
Why Cosmos?
---

__It's simple__

Cosmos is simple to use. It's meant to allow for code as simple as `x=2` or `print('hello world')`.

Cosmos is a general-purpose language that focuses on high-level scripting.

__Multiple styles__

Cosmos takes inspiration from many languages and allows for a variety of styles which includes features from,

- Functional programming,
- Logic programming,
- Prototypal and procedural programming,

The user may adopt a functional, logic or even [procedural](https://github.com/cosmos-lang/cosmos-lang.github.io/wiki/Pseudo-imperative-programming) style.

It's _not_ an opinionated language by any means-which many languages nowadays are becoming, and instead lets the user write extremely non-restricted code. A programmer might make use of mode and type declarations. If they don't, variables are local-by-default and the type is inferred by the language.

__Pure logic programming__

Perhaps its most novel feature is that Cosmos is a legitimate _logic programming language_. It's our view of what modern day logic programming with a redone syntax would look like.

In particular, it focuses on _pure logic programming_. If the user makes a relation, it's pretty much guaranteed to be a pure relation (as cKanren, etc.).

If they don't, it's still a pure function or simply a procedure.

A lot of it is experimental or taken from other logic programming languages (Prolog II, III, etc).

__It's not Prolog__

It must be emphasized that Cosmos is _not_ literally Prolog!

A typical Prolog implementation must follow certain conventions for backward-compatibility. However, there are certain limitations this brings. It means, for example, that _they cannot have a sound 'not' operator_. It's not a particularly minimalist language either.

As a new language, we're not bound by any such limitations. A lot of syntax decisions such as making use of whitespace, using modern operators and naming such as `!=`, `>=` and `concat` are possible because of this.

You may see [this](https://github.com/cosmos-lang/cosmos-lang.github.io/wiki/Comparison) for a better comparison.
