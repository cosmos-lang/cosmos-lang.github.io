# Rationale

Why C-style declarations?
---

Nowadays, many languages opt for a peculiar style of declaration.

`let x:Integer=2`

This is very unlike ours.

`Integer x=2`

This is also a case of applying the precepts.

This is a case where both styles rank equal on familiarity. Any of them could be said to be familiar enough to a programmer by now.

However, there's at least **one** extra keyword and more syntax in the former. It's more cluttered for reasons that arguably aren't worth it.

The second is simpler syntactically and semantic-wise.

Going further into everything between _var_ and _let_ decidedly strays further from making a minimalist or at all user-friendly language.

It's even worse with function declaration. An additional arrow along with an `:` for every argument.

- More keywords.
- More syntax clutter.
- More to read _and_ write.

We've strayed way too far from an user-friendly language for scripting.

Economy of space
---

With all that said, it should be clearer what our ideas and rationale for the language is.

- Whitespace.
- C-style declarations.

These all get a bonus from economy of space. Simply put, a language is less smooth if there's more to type. They get +1 to smooth/minimalist and don't have many drawbacks to offset.

Conventions
---

- camelCase.

Although we have nothing against using_underlines, default libraries will often default 

Disclaimer
---

There's always an element of opinion and interpretation in any discussion regarding syntax or conventions for a language.

What makes a language simple? How far should we go if we want a minimal language?

Nonetheless, this is our particular stance.
