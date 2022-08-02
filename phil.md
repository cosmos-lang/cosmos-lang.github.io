
Why Cosmos?
---

Why a new language? What can it be used for? This tends to be a common question for any new language.

__As a scripting language__

Cosmos takes inspiration from many languages, specially scripting ones. The syntax compares well to common scripting languages.

It's a language that's very readable, simple and concise.

Cosmos is a good general-purpose _scripting language_. It fares well for scripts, prototyping or high-level applications.

Many languages nowadays are becoming overly complex and opinionated. Cosmos strives to go back to what scripting languages were known for. It's simple and flexible allowing for many styles of programming.

__As a functional language__

It's a goal of us to ensure Cosmos can be used as a legitimate _functional language_. It's provided with constructs like closures and a focus on immutability.

__As a logic language__

Cosmos is a legitimate _logic programming language_. It's our view of what modern day Prolog would look like.

It's entirely possible to use it as a regular language, however, and use logic features such as non-determinism only when necessary.

Cosmos is designed so that even if you use write code with an entirely procedural mindset, it will have a functional and logic meaning.

__An academic language?__

Declarative languages are often used academically.

Cosmos covers all main paradigms and even advanced concepts such as functors while benefitting from a more recognizable syntax.

It's not Prolog
--

As a _logic programming language_ based on Prolog, Cosmos can be easily compared to Prolog. It's not Prolog, of course!

Many features of ancient, classic Prolog (such as variables needing to be uppercase) did arguably not age well and are not common today.

Overall, we did not adopt those.

Philosophy
----

The philosophy of the Cosmos programming language can be summed in a few precepts, which the language was designed around,

- Experimental
- Familiarity
- Minimalism
- Smooth

Of course, those precepts are weighted against each other.

Experimental vs Familiarity
--

Although Cosmos is ultimately an exploratory language, it uses common syntax naming and conventions when possible.

It's accurate to say that _we do not deviate from the norm if we don't have to_.

So as to be as user-friendly as possible, it uses a procedural syntax with all the common operators you'd expect from one--unless there's a reason not to. It'll not stop us from supporting logic or functional programming.

If it was merely another imperative scripting language, there would be no reason to make it. Plenty of those already exist. On the other hand, functional languages that still support procedural-style programming and syntax are fewer. Furthermore, we simply like the syntax. 

Minimalism vs Smoothness
--

"Make it simple, but not simpler." - Vonn Neumann

The above quote quite describes a minimalist philosophy.

Adopting common syntax sugar is an example of smoothness. It makes our language smooth to program in, which is important, after all. However, simply adding a new operator or syntax for every function there is isn't necessary. It makes the language less readable. 

At the least, they don't follow the same philosophy as ours.

Basic function or relation syntax exists so that we don't need new operators for everything. 

Weighting the Precepts
--

These precepts may of course sometimes clash. Cosmos may choose to explore a paradigm that's not all that common, which may clash against familiarity. We don't want to make our language so minimal that it is unusable-- thus we weight it against the smoothness and experimental factors.

It's not always so, though. You may note a lot of the time features simply fit and go well together. This is ideal.

Why C-style declarations?
---

Nowadays, many languages opt for a peculiar style of declaration.

`let x:Integer=2`

This is very unlike ours.

`Integer x=2`

This is also a case of applying the precepts.

This is a case where both styles rank equal on familiarity. Any of them could be said to be familiar enough to a programmer by now.

However, there's at least **one** extra keyword and more syntax in the former. It's more cluttered for reasons that arguably aren't worth it.

The second is simpler syntactically and semantic-wise. While syntax is always a matter of opinion, it's definitely less minimalist in our interpretation.
