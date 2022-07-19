
Casting as Abstraction
----

Cosmos' arithmetic system is a bit intricate. Let's try summing up two numbers.

```
x=1+2
print(x) //1+2
```

This occurs because the arithmetic operators are actually functors with special syntax. 1+2 really is a functor of type _Math Integer Integer_ rather than an actual _Integer_.

In order to get the intended result, we must then convert this functor to an _Integer_. This is where we use _casting_.
```
print(int(x)) //3
```
Let's look at the following code,
```
x='c'+y
y='d'
print(str(z)) //'cd'
```

Because we are using functors, we can write logically pure code that sums up strings (naturally, string arithmetic is supported in Cosmos™ ) even if one or more of the parameters is not defined at the time. Note that _y_ is only defined in the second line.

Only at the end of the program do we need to compute the result, if we need to- for example, in order to write it on the screen. 

Prolog has, to say the least, a very poorly thought-out arithmetic system.
- An operator is used instead, making it unclear that 1+2 and 3 are different types.
- The operator is called `is`. Suffice to say, this is misleading in a logic programming language that has an `=` operator to boot.
- While this allows for logically pure code in some ways, that's not always the case. 1+2=3 evaluating to false is an example.

Prolog tries to have its cake and eat it too in how it tries to treat arithmetic. It's unsure on whether to treat 1+2 as a number or not. This is done to make a logically sound system but it ends up being unsound in some ways.

Cosmos inherits this system somewhat, as Prolog is its host language. However, 
- Erroneous results can be better dealt with in a typed language (for example, 1+2=3 is simply a type error).
- We use casting as it's a better metaphor for the whole thing.

Constraints (CLP)
----

CLP or constraint logic programming is a kind of sub-paradigm in modern LP. As such, we felt we should address this sooner or later.

Even regular LP implements logical equality, i.e. `x=2`. This is what we may call an _equality constraint_ when talking about the paradigm.

What about `x!=2`, `x>2`, `x>=2` and so on? CLP addresses those aswell, making them equally valid constraints that are added to a _constraint store_. Note that in a normal language, any of these would fail if x is not instantiated.

This should let you write,

```
>x>2 and x=5
| x=5
>x<2 and x=5
| false
```

Casting to a _real_ or _num_ (as seen in Casting as Abstraction) should also trigger constraint arithmetics.

`x=real(2*4)`

No language that we know has constraints _by default_. What we mean is that if the user has to load external libraries and the default operators (in our case, !, <, >=, etc.) use something else, it can hardly be said that the language implements the paradigm natively. It's a second-class paradigm in the language.

This seems like a waste, however. And Cosmos™ is the perfect language for it, as all we want is a scripting language that works logically _by default_.

As such, Cosmos™ has constraints as the default modum operandis. You may freely try the paradigm as part of regular programming.

Our criteria for a CLP system was humble.

- It should work under both the Reals and Integers.
- It should work on "normal cases".

Our idea of "normal cases" is cases where even a classical non-CLP system would work, i.e. x is instantiated. It should do at least this much if we're making it the default arithmetics of the language, after all. It shouldn't be _worse_ than classical arithmetics.

This does exclude quite a few libraries that use CLP for integers only, or other more specific uses. As such, we borrowed a CLP(R)--or CLP for Reals--library, with floating point numbers. 

From what we know, in classical usecases constraints are not added to the store and thus don't consume extra memory, meaning there's no downside other than an extra check. It's just like a BigNum library!

Still, we are deeming this _experimental_ only because we don't know of other languages that do this. As far as we are aware, we've given enough reason to go CLP-by-default. Other languages should be answering why they _aren't_ CLP-by-default! We believe backwards-compatibility is often the only reason.

print vs write
----

Cosmos is an user-friendly language. It would not be very user-friendly to not have a ready, general-purpose `print` statement. As such, a `hello world` can be written as,

`print('hello world')`

Note that this will output,

`'hello world'`

While `io.writeln('hello world')` will output,

`hello world`

In short, `write` outputs to the user and is the relation to use in a proper program while `print` can still be used for debugging or short scripts.


Host
----

Cosmos is currently compiled into Prolog. As such, it's possible to call predicates of Prolog from Cosmos.

```
rel write(x)
    pl::write(x) //calls Prolog predicate 'write'
```


Using Cosmos within Prolog
----
It's possible to do the opposite, that is, embedding Cosmos in a Prolog program.

See the Swi-Prolog [page](https://www.swi-prolog.org/pack/list?p=cosmos) for more information.
