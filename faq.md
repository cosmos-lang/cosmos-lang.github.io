
Why Cosmos?
---

Cosmos is a highly ambitious language. It's hard to sum up in one sentence, but it aims to,

- Look and function as your average _scripting language_. See the syntax and [Pseudo-imperative programming].
- Work as a functional language with immutability, closures and type-checking.
- Explore pure logic programming. It can be seen as a modern take on Prolog.
- _...with objects._

It's suited for scripting or high-level applications.

Academic-wise, it covers all main paradigms and even advanced concepts such as functors while benefitting from a more recognizable syntax.

What is a functor?
----

Most Prolog tutorials simply explain functors as being _structures_ or "composite data". Effectively, they're very similar to what's known as `named tuples`. You may in fact just consider them tuples.

The use of the word in Prolog predates the functional use of the word. Despite this, many of the same patterns can be used regardless of whether it's functional or language programming we're talking about. It seems being typed makes logic functors very similar to functional functors.

But what is a functor? You're free to think about this whether it is from a philosophical, mathematical or historical perspective.

Cosmos, however, is only interested in this from a pragmatic perspective. It's enough that we can use them as a language feature to implement lists and other structures. We don't ask "what is a for-statement?". We simply use for-statements.

Is this really a functor?
---

We stress that Cosmos functors simply compile to Prolog functors. Even in the C implementation, they use the same bytecodes Prolog uses for functors. This would indicate they're functors, still, this always seems to spur some doubts anyway.

That's even less interesting than the first question! It's utterly pointless.

We don't ask "is this really a for-statement?" for every language that has a slightly different for-statement.

We're only interested in them from a pragmatic perspective.

Should it be called a functor?
----

While we considered renaming them to _tuples_, functors is how programming at large calls them.

Seriously, stop asking about functors.
