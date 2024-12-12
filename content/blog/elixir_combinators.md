+++
title       = "Elixir Combinators"
date        = 2024-12-12
description = """
Combinators are a central concept in functional programming, and one of the most interesting
rabbit holes one can fall down is that of combinatory logic, and the use of the SK(I) Combinator
Calculus for powerful function manipulation.
"""
[taxonomies]
tags = ["combinators", "fp", "elixir"]
+++

## Combinatory Logic & The SK(I) Combinator Calculus

This is a **paragraph** with some additional text 😄 and also some _`verbatim text`_. What happens if a line goes longer, I wonder? Where do we hit the newline word wrap? Does it stop widening the main text area?

$\lnot P \land \lnot Q = \lnot (P \lor Q)$

$\lnot P \lor \lnot Q = \lnot (P \land Q)$

Looks like math doesn't render currently 😦.

---

## The Primary Combinators

These combinators are being defined uncurried as Elixir doesn't use the automatic currying approach.
In many contexts, the power of combinators is best expressed in an ML/Miranda descended language or
and array language like APL, J, or BQN.

- I
- Identity
- Id
- Idiot
- Ibis

<!--can do `elixir,linenos,linenostart=10,hl_lines=3-4 8-9,hide_lines=2 7`-->

```elixir
# a -> a
def idiot(a) do
  a
end
```

- K
- Kestrel
- Constant
- True
- Left

```elixir
# a -> b -> a
def kestrel(a, b) do
  a
end
```

- S
- Schmeltzen, 'to fuse'
- Starling
- ap
- <\*>

```elixir
# (a -> b -> c) -> (a -> b) -> a -> c
def starling(a, b, c) do
  a(c, b(c))
end
```
