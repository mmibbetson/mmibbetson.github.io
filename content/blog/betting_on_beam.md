+++
title       = "Betting on BEAM"
date        = 2024-12-20
description = """
Bogdan/Björn's Erlang Abstract Machine is the virtual machine for Erlang, Elixir, LFE, and Gleam.
It's also an historic piece of engineering with so much to teach about concurrency, parallelism,
fault tolerance, and distribution.
"""
[taxonomies]
tags = ["beam", "elixir", "erlang"]
+++

## A Strange Journey

### What Are We Doing?

**Bogdan/Björn's Erlang Abstract Machine** (BEAM) is the virtual machine that powers the Erlang and Elixir programming languages, among others. I first came across it through a [Computerphile Video](https://www.youtube.com/watch?v=SOqQVoVai6s) at the beginning of my journey into functional programming. Initially, many of its virtues went over my head. But in time (and with a ravenous addiction to watching talks from [Strange Loop Conferences](https://www.youtube.com/@StrangeLoopConf)) I came across a few talks that shifted my entire perspective on programming after spending some time in the real world of software development.

It was [Joe Armstrong](<https://en.wikipedia.org/wiki/Joe_Armstrong_(programmer)>)'s talk called [The Mess We're In](https://www.youtube.com/watch?v=lKXe3HUG2l4) which first had a hand in this shift. Joe was one of the co-creators of Erlang, and this talk, I feel, illustrates the relevance of its concerns around the dire state of modern computer programs to modern computer programmers very effectively. He uses his background in physics and his depth of experience in programming to discuss mainstay computing concerns such as performance, complexity, documentation, and so on, while consistently injecting both humorous and enlightening insights at every turn. I was so taken by this talk that I felt I had to see more from him, and this is when things really changed for me.

### Systems That Run Forever

The talk [Systems That Run Forever, Self-Heal, and Scale](https://www.youtube.com/watch?v=cNICGEwmXLU) is one that I consider **essential viewing** for any programmer with the slightest passion for their craft or financial incentive to build fault tolerant systems.

In this talk, Joe shows how the actor model mirrors parallelism in the real world, considers the difficult problem of distributed data and computation, presents _real solutions_, and expounds on the importance of recoverability and fault tolerance. For me, the greatest takeaway from this is the following: If you want fault tolerance, _you **must** have distributed systems_. This is because you can't have fault tolerance on a single machine - what happens if that machine breaks? Forces beyond the programs we write can take down our infrastructure at any moment. Therefore, we require redundancy as a protection against failure. As soon as we have two machines, we have a concurrent, distributed program.

It's not much help for me to just regurgitate points better made by the man himself, so rather than go through each and every bit of information in the talk, I'll just highlight hereafter one particularly important section summarily - what Joe calls the "Six Rules of Wault Tolerant Systems".

#### Isolation

Isolation is the most important of these rules. It enables reliability through the independence of processes, scalability through horizontal expansion, and both testability and comprehensibility through clear boundaries of factoring.

#### Concurrency

If a system is based on isolated process, it must necessarily be able to describe its behaviour in a concurrent manner as those processes carry out their individual functions. Concurrency is desirable because many problems are inherently parallel, such as the problem of fault tolerance requiring multiple machines discussed earlier.

#### Failure Detection

Failure is going to happen in any system. Some failures are detectable at compile-time, but a great many aren't. It might be nice to have my type system tell me that my computer is going to be struck by lightning at some point during compile-time but we don't have that ability quite yet, nor would it actually solve the problem. If you can't detect the failure, you can't fix it. This failure detection needs to work across process boundaries because failed processes can't locally repair themselves.

#### Fault Identification

To properly resolve failures, we have to know why and how they happened, not just _that_ they happened. Proper fault identification implies sufficient information to be used in post hoc debugging of failures, which can be used in live code upgrades to fix running systems.

#### Live Code Upgrade

Trailing from the previous rule, live code upgrade is necessary to allow systems to "run forever". Atomic stop-and-restart is extremely undesireable for distributed systems, and with isolation the idea that we must disable the functioning majority of our processes to triage the faulty few is quite obviously absurd.

#### Stable Storage

Stable storage is not a concern only of the language and runtime, it touches many layers of a system, but the ability to have distributed, stable data is essential for true fault tolerance. Missing or corrupted data (i.e. information) is a rather significant problem in _information_ technology. At one point in the talk, Joe says the following:

> "Data is sacred and computation isn't. You really need to look after your data and make sure you never lose it. Computation, that's just stuff that transforms data. If the program crashes just re-run it or something like that; that's not a problem - you can run a computation anywhere, provided you can get hold of the data."

### What Does This Actually Look Like?

Although this is all terribly relevant to anyone working with distributed systems today, it's still a little bit inconcrete in that it's a conversation about the technology and not a direct demonstration of the technology itself. Much of the time these things don't fully _'click'_ for us until we see them in action. Saša Jurić does a fantastic job of giving a concrete, live demonstration of these mechanisms in [The Soul of Erlang and Elixir](https://www.youtube.com/watch?v=JvBT4XBdoUE). Witnessing the scheduler, supervisors, and recoverability in action gives a real sense of how transformative this model is for real-world systems.

## Finding Footholds

> "So if this is such incredible technology, why is nobody using it?"

I had thought this initially, before I came to learn that, really, _practically everybody_ is using it. It arrived, solved a very important problem, and then kept on quietly solving that problem for the last 30+ years. The growing vocal interest in it presently is likely best explained by the increasing need for robust systems at scale and the frequent problems posed by concurrency in other languages, as well as the decline of [Koomey's Law](https://en.wikipedia.org/wiki/Koomey%27s_law) pushing us to reach for parallelisation in search of greater performance gains.

But I digress, I mentioned that everybody is using the BEAM. Is this true? Well, according to Joe Armstrong ca. 2013, Erlang is used in about [half of the world's telecoms infrastructure](https://www.youtube.com/watch?v=cNICGEwmXLU&t=600s). [WhatsApp](https://www.erlang-solutions.com/blog/20-years-of-open-source-erlang-openerlang-interview-with-anton-lavrik-from-whatsapp/) has used Erlang for a very long time, and [Discord](https://elixir-lang.org/blog/2020/10/08/real-time-communication-at-scale-with-elixir-at-discord/) is known to get immense value from Elixir. Discord has contributed some great work to the Elixir ecosystem as well, like [Manifold](https://github.com/discord/manifold) and [Semaphore](https://github.com/discord/semaphore). [Fly.io](https://fly.io/), in particular, and their use of [FLAME](https://fly.io/blog/rethinking-serverless-with-flame/) are very exciting (relatively) recent developments.

On top of this, there are numerous high-quality learning resources developed by core contributors and often even the creators of these languages ranging from learning the languages to learning about their important libraries, designing systems that scale, metaprogramming, and more. The community that has built up around the BEAM is full of experts and an oasis of friendliness in the metaphorical desert that is programming language discourse. That being said, if that weren't the case I don't feel it would diminish the value of the technology - it's just a pleasant addition to an already overwhelming number of reasons to appreciate it.

### BEAM Languages

Thus far, I've spoken almost entirely about the virtual machine itself and not about the languages that compile to BEAM bytecode. This is because the virtual machine really is the **most** important part, but it is not the **only** important part. Luckily, if you're a picky programmer with a preference for particular syntax, there are multiple viable languages to choose from.

The original language for the Erlang Abstract Machine is, of course, _[Erlang](https://www.erlang.org/)_, with its Prolog-inspired syntax:

```erl
hello_world() ->
  io:format("Hello world!~n").
```

These days the common BEAM language of choice for many domains is _[Elixir](https://elixir-lang.org/)_, and there are many good reasons for this: powerful metaprogramming capabilities, friendly syntax, expressive pattern matching, and amazing documentation. Its syntax is descended from Ruby's:

```ex
def hello_world() do
  "Hello world!" |> IO.puts
end
```

If you do not burst into flame in the vicinity of S-expressions and enjoy working with a lisp, there's _[Lisp-Flavoured Erlang](https://lfe.io/)_:

```lisp
(defun (hello_world)
  (io:format "Hello world!~n"))
```

For people who crave C-style braces or feel a need for static types, there's also _[Gleam](https://gleam.run/)_ which layers Rust's syntax onto SML/OCaml/F#'s semantics (bar currying-by-default) and the BEAM's execution model:

```rust
fn hello_world() {
  "Hello world!" |> io.println()
}
```

The growth of any of these languages benefits the others due to the interoperability afforded by their shared virtual machine. The most obvious example here is that all of these languages utilise the Erlang Open Telecom Platform as the basis of their concurrency systems.

## Reaching New Heights

Although some familiarity with Erlang is beneficial no matter which language you choose to use (it is the _Erlang_ Abstract Machine, after all), I feel that, upon inspection, Elixir is the clear frontrunner for potential growth and utility over the next decade.

There are several very exciting developments going on in the Elixir ecosystem, from StackOverflow's most-loved web framework for two consecutive years, [Phoenix](https://www.phoenixframework.org/), to the numerical computing project [Nx](https://github.com/elixir-nx) which is rapidly growing the presence of the language in the machine learning and data science space. Nx also includes the amazing [Livebook](https://livebook.dev/), which is something of an analogue to Jupyter Notebook. [Nerves](https://nerves-project.org/) is the final community project that I'll mention here - a framework for creating software for embedded devices. This is exciting for those of us who are usually confined entirely to writing to web services or command-line tools but would like to have a familiar environment in which we can learn about embedded programming.

There has been a lot of work done by José Valim, Giuseppe Castagna, and Guillaume Duboc in recent years to develop a gradual type system for Elixir, which has resulted in new research on [Set-Theoretic Gradual Types](https://arxiv.org/abs/2306.06391). This has already begun its integration into the Elixir ecosystem, and I believe will serve to improve adoption by programmers who prefer not to use dynamically typed languages (beyond the actual concrete value proposition of opt-in compile-time type checking eliminating certain types of errors).

## Do Not Look Down

The adage that there is _"No silver bullet"_ is among the most frequently espoused programmer heuristics, and it's true that we have no tools that solve _every_ problem. In fact, we have many tools which solve no problem at all. Erlang was created to solve a _particular_ problem: distributed programming; as it so happens, most programming today involves distributed systems.

When considering the proverbial impurities in the BEAM's metal, it turns out that you can squeeze a lot of performance and comfort from programming languages that ignore the central concerns of distributed programming, much like making simplifying assumptions can aid the clarity and conciseness of scientific or mathematical proofs at the expense of correctness and comprehensiveness. Sometimes this is an acceptable, or (more rarely) necessary exchange. This means that the BEAM is neither the most performant nor the most popular environment.

### Soft-Real-Time

A performance goal of the BEAM is that it aims to achieve "soft-real-time" performance. It's not suited to hard-real-time programs the way Rust is, for example. There is a cost to its concurrency semantics, low as it is, and it is a garbage-collected runtime. Because much of this overhead is designed to tolerate large-scale systems, there is an efficiency loss in scaling down to single-process environments where other garbage-collected languages will sometimes outperform Elixir or Erlang.

The cost-benefit analysis becomes less grim when considering that, generally, performance constraints on the kinds of single-threaded, synchronous programs written in high-level languages are effectively inconsequential. If we can glue our operating systems together with Python, there's certainly no need to fear the performance of Elixir in these contexts.

Additionally, in the domain these languages are designed for, they look far more appealing next to their competitors. Benchmarks, in general, are difficult to run well, and even more difficult to trust. That said, if you have the time and curiosity, [this article](https://www.erlang-solutions.com/blog/comparing-elixir-vs-java/) demonstrates the broad comparison of a BEAM language against a non-BEAM language in a context that is relevant (network-bound, mixed-workload, concurrent systems). In the future, I imagine that the [aforementioned decline](#finding-footholds) of Koomey's Law will play a role in seeing languages which parallelise processes more easily become more performant in ways others can't.

### It's All About Popular

Fashion has been an ever-fickle guiding hand in programming history since its inception, with just as much power as any meritocratic assessment of technologies, if not more. BEAM languages, by comparison to other programming language communities like Python, JavaScript, and so on, have a smaller ecosystem. It's not terribly small, though - you'd have an easier time finding an Elixir programmer than, say, a [Janet](https://janet-lang.org/) programmer. The oft-cited "friendly syntax" of Elixir goes a long way in amplifying learner enthusiasm and there is even an [entire book](https://pragprog.com/titles/tvmelixir/adopting-elixir/) on the process of adopting the language and onboarding teams.

With the current growth Elixir is experiencing and the large existing role Erlang has in the computing and telecommunications industries, I don't feel that this concern holds up to scrutiny unless it is absolutely _essential_ that you work with only the most fashionable languages. There are circumstances where this might genuinely be the case, but I am doubtful that it is the majority of situations.

## Summit

There's so much more to be said about the BEAM, Erlang, Elixir, all of the amazing open source work being done with them, and the historical significance of their contribution to human communication. Far more than could reasonably be covered here. I feel so convinced of its importance and its very necessary place in the kinds of programs we write today, that I'm compelled to end on a variation of [Greenspun's Tenth Law](https://en.wikipedia.org/wiki/Greenspun%27s_tenth_rule) when considering how we often try to replicate the benefits of the BEAM by duct-taping various external tools to together with YAML and bolting the resulting behemoth onto our programs:

> "Every sufficiently complicated distributed program contains an ad hoc, informally-specified, bug-ridden, slow implementation of half of the BEAM."
