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
information technology. I first came across it through a [Computerphile Video](https://www.youtube.com/watch?v=SOqQVoVai6s) in the beginning of my journey into functional programming. Initially, many of its virtues went over my head. But in time (and with a ravenous addiction to watching talks from [Strange Loop Conferences](https://www.youtube.com/@StrangeLoopConf)) I came across a few talks that shifted my entire perspective on programming after spending some time in the real world of software development.

Initially, I had simply been on a regular Strange Loop binge and stumbled upon [Gerald Sussman](https://en.wikipedia.org/wiki/Gerald_Jay_Sussman)'s talk [We Really Don't Know How to Compute!](https://www.youtube.com/watch?v=HB5TrK7A4pI) As with most things Dr. Sussman has done it completely blew my mind, and it became more pertinent with every passing day as I dealt with information systems riddled with unmitigated decay. That said, the ideas in that talk have a somewhat academic bent (anathema to the industry programmer) and I'm convinced that there are _hordes_ of programmers that spontaneously combust upon seeing an S-expression. Lack of familiarity breeds resentment even in programming languages, I suppose.

Fortunately, [Joe Armstrong](<https://en.wikipedia.org/wiki/Joe_Armstrong_(programmer)>) (one of the creators of Erlang) has a talk in much the same vein called [The Mess We're In](https://www.youtube.com/watch?v=lKXe3HUG2l4). This talk, I feel, illustrates the relevance of its concerns to industry programmers more directly. Joe uses his background in physics and his depth of experience in programming to discuss mainstay computing concerns such as performance, complexity, documentation, and so on, while consistently injecting both humorous and enlightening insights at every turn. I was so taken by this talk that I felt I had to see more from him, and this is when things really changed for me.

### Systems That Run Forever

The talk [Systems That Run Forever, Self-Heal, and Scale](https://www.youtube.com/watch?v=cNICGEwmXLU) is one that I consider **essential viewing**.

- actor model (byzantine generals problem)
- scalability (scheduler, serialiseable data structures)
- error handling (supervisors, let it crash, recoverability)
- there are costs
- not the fastest (but soft-real-time)
- not the largest ecosystem
- but it is RELIABLE, and everywhere else you need to BOLT ON things outside of the language that then need to consider the behaviour of your program to reproduce the same behaviour that BEAM will, except buggier and with more network calls.

Saša Jurić does a fantastic job of giving a concrete, live demonstration of these mechanisms in [The Soul of Erlang and Elixir](https://www.youtube.com/watch?v=JvBT4XBdoUE). Witnessing the scheduler, supervisors, and recoverability in action gives a real sense for how transformative this model is for real-world systems.

## Finding a Foothold

So if this is such incredible technology, why is nobody using it? I had thought this initially, before I came to find that, really, **everybody** is using it. It arrived, solved a very important problem, and then kept on solving that problem for the last 40 years. The growing interest in it presently is likely best explained by the increasing need for robust systems at scale and the frequent problems posed by concurrency in other languages, as well as the decline of [Koomey's Law](https://en.wikipedia.org/wiki/Koomey%27s_law) pushing us to reach for parallelisation in search of greater performance gains.

But I digress, I mentioned that **everybody** is using BEAM. Is this true? Well, according to Joe Armstrong ca. **TODO**, Erlang is used in about half of the world's telecoms infrastructure[^erlang-use]. WhatsApp has used Erlang for a very long time[^whatsapp-erl], and Discord is known to get immense value from Elixir[^discord-ex]. They have contributed some great work to the Elixir ecosystem as well, like [Manifold](https://github.com/discord/manifold) and [Semaphore](https://github.com/discord/semaphore). [Fly.io](https://fly.io/), in particular, and their use of [FLAME](https://fly.io/blog/rethinking-serverless-with-flame/) are very exciting (relatively) recent developments.

On top of this, there are numerous high-quality learning resources developed by core contributors and often even the creators of these languages ranging from learning the languages to learning about their important libraries, designing systems that scale, metaprogramming, and more. The community that has built up around the BEAM is full of experts and a relative wealth of friendliness and dearth of hostility. That being said, if that weren't the case I don't feel it would diminish the value of the technology - it's just a pleasant addition to an already overwhelming number of reasons to appreciate it.

### BEAM Languages

- TODO: add a little introduction

The original language for the Erlang Abstract Machine is, of course, _[Erlang](https://www.erlang.org/)_, with its Prolog-inspired syntax:

```erl
hello_world() ->
  io:format("Hello world!~n").
```

These days the common BEAM language of choice for many domains is _[Elixir](https://elixir-lang.org/)_, and there are many good reasons for this: powerful metaprogramming capabilities, friendly syntax, expressive pattern matching, and amazing documentation. Its syntax is descended from that of Ruby:

```ex
def hello_world() do
  "Hello world!" |> IO.puts
end
```

If you (like me) **do not** burst into flame in the vicinity of S-expressions and enjoy working with a lisp, there's _[Lisp-Flavoured Erlang](https://lfe.io/)_:

```lisp
(defun (hello_world)
  (io:format "Hello world!~n"))
```

For people who can't give up their C-style braces or feel that they need static typing, there's also _[Gleam](https://gleam.run/)_ which layers Rust's syntax with SML/OCaml/F#'s semantics (bar currying-by-default) and BEAM's execution model:

```rust
fn gleam_example() {
  "Hello world!" |> io.println()
}
```

The growth of any of these languages benefits the others due to the interoperability afforded by their shared virtual machine. The most obvious example here being the fact that all of these languages utilise the Erlang Open Telecom Platform as the basis of their concurrency systems.

## Reaching New Heights

Although some familiarity with Erlang is beneficial no matter which language you choose to use (it is the _Erlang_ Abstract Machine, after all), I feel that, upon inspection, Elixir is the clear frontrunner for potential growth and utility over the next decade.

- elixir's serious growth with phoenix, nerves, nx, livebook

- set-theory based gradual type system

## References

[^erlang-use]: Armstrong, Joe. (TODO). TODO. Strange Loop.

[^whatsapp-erl]: TODO. (TODO). TODO. TODO.

[^discord-ex]: TODO. (TODO). TODO. TODO.
