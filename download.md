# Installation

## As an Executable

Cosmos can be installed by, (1). Installing Swi-Prolog (v7+), (2) downloading the [latest release](https://github.com/mcsoto/cosmos-lang/releases/tag/v0.13.3-alpha), and (3) simply typing,

```
make
```

in the project directory.

This should work on any system that can run Swi-Prolog.

You can test that the installation has succeeded.

```
$ cosmos -v
"Cosmos 0.13 beta - (Pl)"
```

## Pack

Cosmos can be installed as a Swi-Prolog pack. This is recommended if you are already a Prolog user or plan to use the languages together.

```
:- pack_install(cosmos).
```
You can then load the language.
```
:- use_module(library(cosmos)).
:- cquery('x=2').
```
If you want to open the interpreter:
```
:- cstart.
```

As said, this is recommended if you're already a Prolog user. You're opening the Cosmos interpreter inside the Prolog interpreter, and so on. This is somewhat redundant. 

Naturally, you may install it both normally and as a pack.


