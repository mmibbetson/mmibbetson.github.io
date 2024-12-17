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

- came across erlang first through computerphile learning about fp
- after falling in love with Strange Loop Conference, I watched and rewatched Joe Armstrong's talks
- Sasa Urić's talk teh soul of erlang and elixir
- safety, recoverability, self-healing, scale, soft-real-time
- elixirs growing ecosystem
- erlangs strong hold in the existing infrastructure
- incredible wealth of literature

### Languages

These days the common BEAM language of choice seems to tend toward [Elixir](https://elixir-lang.org/), and there are many good reasons for this - powerful metaprogramming capabilities, friendly syntax, expressive pattern matching, and amazing documentation. Its syntax is descended from that of Ruby:

This here is another paragraph to test some spacing.

```erl
def elixir_example() do
  "like this," |> print()
end
```

The original language for the Erlang Abstract Machine is, of course, [Erlang](https://www.erlang.org/), with its Prolog-inspired syntax:

```ex
erlang_example() ->
  print("like this,").
```

If you enjoy homoiconicity and the uniformity of S-expressions like I do, there's [LFE](https://lfe.io/):

```lfe
(defun (lfe-example)
  (print "like this,"))
```

For people who can't give up their C-style braces and don't mind working with a very young language, there's also [Gleam](https://gleam.run/) (which sits somewhere between Rust and SML/OCaml/F# syntactically):

```gleam
fn gleam_example() {
  "like this," |> print()
}
```

The value proposition of Gleam is that it uses a static type system with Hindley-Milner style type inference to guarantee certain program invariants at compile-time. This is of course a very nice tool to have in some systems and scenarios. It is not to my liking, however, both in terms of its approach to type safety and syntax.
