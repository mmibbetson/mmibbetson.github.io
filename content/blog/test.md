+++
title       = "My Test Post"
date        = 2024-11-24
description = """
This is my first test post to the blog section of the site.
I am filling the description with a lot of detail as I
intend for this to hit the maximum width.
"""
[taxonomies]
tags = ["test", "foo", "bar", "this is a real long one", "whatever", "etc"]
+++

This is a **paragraph** with some additional text 😄 and also some _`verbatim text`_. What happens if a line goes longer, I wonder? Where do we hit the newline word wrap? Does it stop widening the main text area?

$\lnot P \land \lnot Q = \lnot (P \lor Q)$

$\lnot P \lor \lnot Q = \lnot (P \land Q)$

Looks like math doesn't render currently 😦.

## Code Fence

Here's some rust:

```rs
pub fn main() {
    println!("Hello, Blog!");
}
```

And here's some elixir:

```elixir
def concat_style(prefix) do
  prefix <> "style!"
end
```
