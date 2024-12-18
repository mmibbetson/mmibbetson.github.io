+++
title       = "Betting on BEAM"
date        = 2024-12-17
description = """
Bogdan/Björn's Erlang Abstract Machine has been called the "soul of Erlang and Elixir." In this post 
I discuss how and why I will be investing my time into working with BEAM technologies for building
information systems that make sense.
"""
[taxonomies]
tags = ["beam", "elixir", "erlang"]
+++

## A Strange Journey

### What Are We Doing?

**Bogdan/Björn's Erlang Abstract Machine** seems to be something of a sleeper hit in the world of
information technology. I first came across it through a [Computerphile Video](https://www.youtube.com/watch?v=SOqQVoVai6s) in the beginning of my journey into functional programming. Initially, many of its virtues went over my head. But in time (and with a ravenous addiction to watching [Strange Loop Talks](https://www.youtube.com/@StrangeLoopConf)) I came across a few talks that shifted my entire perspective on programming after spending some time in the real world of software development.

Initially, I had simply been on a regular Strange Loop binge and stumbled upon [Gerald Sussman](https://en.wikipedia.org/wiki/Gerald_Jay_Sussman)'s talk [We Really Don't Know How to Compute!](https://www.youtube.com/watch?v=HB5TrK7A4pI) As with most things Dr. Sussman has done it completely blew my mind, and it became more pertinent with every passing day as I dealt with information systems riddled with unmitigated decay. That said, the ideas in that talk have a somewhat academic bent (anathema to the industry programmer) and I'm convinced that there are _hordes_ of programmers that spontaneously combust upon seeing an S-expression. Lack of familiarity breeds resentment even in programming languages, I suppose.

Fortunately, [Joe Armstrong](<https://en.wikipedia.org/wiki/Joe_Armstrong_(programmer)>) (one of the creators of Erlang) has a talk in much the same vein called [The Mess We're In](https://www.youtube.com/watch?v=lKXe3HUG2l4). This talk, I feel, illustrates the relevance of its concerns to industry programmers more directly. Joe uses his background in physics and his depth of experience in programming to discuss mainstay computing concerns such as performance, complexity, documentation, and so on, while consistently injecting both humorous and enlightening insights at every turn. I was so taken by this talk that I felt I had to see more from him, and this is when things really changed for me.

### Systems That Run Forever

- safety, recoverability, self-healing, scale, soft-real-time

The talk [Systems That Run Forever, Self-Heal, and Scale](https://www.youtube.com/watch?v=cNICGEwmXLU) is one that I consider **essential viewing**.

- actor model (byzantine generals problem)
- scalability (scheduler, serialiseable data structures)
- error handling (supervisors, let it crash)
- there are costs
- not the fastest
- not the largest ecosystem
- but it is RELIABLE, and everywhere else you need to BOLT ON things outside of the language that then need to consider the behaviour of your program to reproduce the same behaviour that BEAM will, except buggier and with more network calls.


Saša Jurić does a fantastic job of giving a concrete, live demonstration of these mechanisms in [The Soul of Erlang and Elixir](https://www.youtube.com/watch?v=JvBT4XBdoUE). Witnessing the scheduler, supervisors, and recoverability in action gives a real sense for how transformative this model is for real-world systems.

## Finding a Foothold

So if this is such incredible technology, why is nobody using it? I had thought this initially, before I came to find that, really, **everybody** is using it. It arrived, solved a very important problem, and then kept on solving that problem for the last 40 years. The growing interest in it presently is likely best explained by the increasing need for robust systems at scale and the frequent problems posed by concurrency in other languages, as well as the decline of [Koomey's Law](https://en.wikipedia.org/wiki/Koomey%27s_law) pushing us to reach for parallelisation in search of greater performance gains.

But I digress, I mentioned that **everybody** is using BEAM. Is this true? Well, according to Joe Armstrong ca. TODO, Erlang is used in about half of the world's telecoms infrastructure[^erlang-use]. WhatsApp has used Erlang for a very long time[^whasapp-erl], and Discord is known to get immense value from Elixir[^discord-ex]. They have contributed some great work to the Elixir ecosystem as well, like [Manifold](https://github.com/discord/manifold) and [Semaphore](https://github.com/discord/semaphore).

- erlangs strong hold in the existing infrastructure
- incredible wealth of literature

### BEAM Languages

These days the common BEAM language of choice is [Elixir](https://elixir-lang.org/), and there are many good reasons for this - powerful metaprogramming capabilities, friendly syntax, expressive pattern matching, and amazing documentation. Its syntax is descended from that of Ruby:

```ex
def hello_world() do
  "Hello world!" |> IO.puts
end
```

The original language for the Erlang Abstract Machine is, of course, [Erlang](https://www.erlang.org/), with its Prolog-inspired syntax:

```erl
hello_world() ->
  io:format("Hello world!~n").
```

If you (like me) do **not** burst into flame in the vicinity of S-expressions there's also [Lisp-Flavoured Erlang](https://lfe.io/):

```lisp
(defun (hello_world)
  (io:format "Hello world!~n"))
```

For people who can't give up their C-style braces and don't mind working with a very young language, there's also [Gleam](https://gleam.run/) (which sits somewhere between Rust and SML/OCaml/F# syntactically):

```rust
fn gleam_example() {
  "Hello world!" |> io.println()
}
```

The **value proposition** of _Gleam_ is that it uses a static type system with Hindley-Milner style type inference to guarantee certain program invariants at compile-time. This is of course a very nice tool to have in some systems and scenarios. It is not to my liking, however, both in terms of its approach to type safety and syntax.

## Reaching New Heights

- elixir's serious growth with phoenix, nerves, nx, livebook
- set-theory based gradual type system

## References

[^erlang-use]: Armstrong, Joe. (TODO). TODO. Strange Loop.
