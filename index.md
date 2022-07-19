## Introduction

Cosmos is a modern logic scripting language with a simple syntax.

```javascript
rel main()
    x = io.read()
    io.writeln("hello, "+x+'!')
```

Cosmos combines features from functional (including type checking), object-oriented and even logic programming.

Relational programming
--

As a logic programming language, Cosmos allows programming using relations. Unlike functions, relations may yield multiple results.

```javascript
> x=1 or x=2
| x=1
| x=2
```

It's possible to fall back from relational programming. The keyword `fun` essentially turns a relation into a regular programming function.

Cosmos is not an opinionated language and supports a variety of styles from functional to plain imperative programming. 

See below.

Documentation
--

See the [Quickstart](https://mcsoto.github.io/cosmos-lang/quickstart.html) or the full [Guide](https://mcsoto.github.io/cosmos-lang/guide.html)*.

The guide is meant to be more comprehensive and eventually provide a full documentation of the language. It may still need some proof-reading. The Quickstart is a quicker intro that assumes you have prior experience with procedural or functional languages.

Download
--

See the [Download](https://mcsoto.github.io/cosmos-lang/download.html) section.

Philosophy
--

See the language's [philosophy](https://cosmos-lang.github.io/phil.html).

Other
--

- [Comparison to Prolog, etc.](https://mcsoto.github.io/cosmos-lang/comp.html)

- [A few more notes (Quickstart 2.0)](https://mcsoto.github.io/cosmos-lang/quickstart2.html)
