+++
title       = "Betting on BEAM"
date        = 2024-12-17
description = """
Bogdan/Björn's Erlang Abstract Machine has been called the "soul of Erlang and Elixir." In this post 
I discuss how and why I will be investing my time into working with the BEAM for building
information systems that make sense.
"""
[taxonomies]
tags = ["beam", "elixir", "erlang"]
+++

## A Strange Journey

### What Are We Doing?

**Bogdan/Björn's Erlang Abstract Machine** (BEAM) seems to be something of a sleeper hit in the world of
information technology. I first came across it through a [Computerphile Video](https://www.youtube.com/watch?v=SOqQVoVai6s) in the beginning of my journey into functional programming. Initially, many of its virtues went over my head. But in time (and with a ravenous addiction to watching talks from [Strange Loop Conferences](https://www.youtube.com/@StrangeLoopConf)) I came across a few talks that shifted my entire perspective on programming after spending some time in the real world of software development.

Initially, I had simply been on a regular Strange Loop binge and stumbled upon [Gerald Sussman](https://en.wikipedia.org/wiki/Gerald_Jay_Sussman)'s talk [We Really Don't Know How to Compute!](https://www.youtube.com/watch?v=HB5TrK7A4pI) As with most things Dr. Sussman has done it completely blew my mind, and it became more pertinent with every passing day as I dealt with information systems riddled with unmitigated decay. That said, the ideas in that talk have a somewhat academic bent (anathema to the industry programmer) and I'm convinced that there are _hordes_ of programmers that spontaneously combust upon seeing an S-expression. Lack of familiarity breeds resentment even in programming languages, I suppose.

Fortunately, [Joe Armstrong](<https://en.wikipedia.org/wiki/Joe_Armstrong_(programmer)>) (one of the creators of Erlang) has a talk in much the same vein called [The Mess We're In](https://www.youtube.com/watch?v=lKXe3HUG2l4). This talk, I feel, illustrates the relevance of its concerns to industry programmers more directly. Joe uses his background in physics and his depth of experience in programming to discuss mainstay computing concerns such as performance, complexity, documentation, and so on, while consistently injecting both humorous and enlightening insights at every turn. I was so taken by this talk that I felt I had to see more from him, and this is when things really changed for me.

### Systems That Run Forever

The talk [Systems That Run Forever, Self-Heal, and Scale](https://www.youtube.com/watch?v=cNICGEwmXLU) is one that I consider **essential viewing** for any programmer with the slightest passion for their craft or financial incentive to build fault-tolerant systems.

In this talk, Joe shows how the actor model mirrors parallelism in the real world, considers the difficult problem of distributed data and computation, presents _real solutions_, and expounds on the importance of recoverability and fault-tolerance. For me, the greatest takeaway from this is the following: If you want fault-tolerance, _you **must** have distributed systems_.

It's not much help for me to just regurgitate points better made by the man himself, so rather than go through each and every bit of information in the talk, I'll just highlight hereafter one particularly important section summarily - what Joe calls the "Six Rules of Fault-Tolerant Systems".

#### Isolation

Isolation is the most important of these rules. It enables reliability through independence of processes, scalability through horizontal expansion, and both testability and comprehesibility through clear boundaries of factorisation.

#### Concurrency

If a system is based on isolated process, it must be able to describe its behaviour in a concurrent manner. Concurrency is desireable because many problems are inherenltly parallel, such as the problem of fault-tolerance! You cannot be fault-tolerant with a single process or even a single computer. If you have two computers, you have a concurrent and distributed system.

#### Failure Detection

Failure is going to happen in any system. Some failures are detectable at compile-time, but a great many aren't. It might be nice to have my type system tell me that my computer is going to be struck by lightning at some point during compile-time but we don't have that ability quite yet, nor would it actually solve the problem. If you can't detect the failure, you can't fix it. This failure detection needs to work across process boundaries, because failed processes can't locally repair themselves.

#### Fault Identification

To properly resolve failures, we have to know why and how they happened, not just _that_ they happened. Proper fault identification implies sufficient information to be used in post hoc debugging of failures, which can be used in live code upgrades to fix running systems.

#### Live Code Upgrade

Trailing from the previous rule, live code upgrade is necessary to allow systems to "run forever". Atomic stop-and-restart is extremely undesireable for distributed systems, and with isolation the idea that we must disable the functioning majority of our processes to triage the faulty few is quite obviously absurd.

#### Stable Storage

Stable storage is not a concern only of the language and runtime, it touches many layers of a system, but the ability to have distributed, stable data is essential for true fault-tolerance. Missing or corrupted data (i.e. information) is a rather significant fault in _information_ technology. At one point in the talk Joe says the following:

> "Data is sacred and computation isn't. You really need to look after your data and make sure you never lose it. Computation, that's just stuff that transforms data. If the program crashes just re-run it or something like that; that's not a problem - you can run a computation anywhere, provided you can get hold of the data."

### What Does This Actually Look Like?

Although this is all terribly relevant to anyone working with distributed systems today, it's still a little bit inconcrete in that it's a conversation about the technology and not a direct demonstration of the technology itself. Much of the time these things don't fully _'click'_ for us until we see them in action. Saša Jurić does a fantastic job of giving a concrete, live demonstration of these mechanisms in [The Soul of Erlang and Elixir](https://www.youtube.com/watch?v=JvBT4XBdoUE). Witnessing the scheduler, supervisors, and recoverability in action gives a real sense for how transformative this model is for real-world systems.

## Finding Footholds

So if this is such incredible technology, why is nobody using it? I had thought this initially, before I came to find that, really, **everybody** is using it. It arrived, solved a very important problem, and then kept on solving that problem for the last 40 years. The growing interest in it presently is likely best explained by the increasing need for robust systems at scale and the frequent problems posed by concurrency in other languages, as well as the decline of [Koomey's Law](https://en.wikipedia.org/wiki/Koomey%27s_law) pushing us to reach for parallelisation in search of greater performance gains.

But I digress, I mentioned that **everybody** is using the BEAM. Is this true? Well, according to Joe Armstrong ca. 2013, Erlang is used in about [half of the world's telecoms infrastructure](https://www.youtube.com/watch?v=cNICGEwmXLU&t=600s). [WhatsApp](https://www.erlang-solutions.com/blog/20-years-of-open-source-erlang-openerlang-interview-with-anton-lavrik-from-whatsapp/) has used Erlang for a very long time, and [Discord](https://elixir-lang.org/blog/2020/10/08/real-time-communication-at-scale-with-elixir-at-discord/) is known to get immense value from Elixir. Discord has contributed some great work to the Elixir ecosystem as well, like [Manifold](https://github.com/discord/manifold) and [Semaphore](https://github.com/discord/semaphore). [Fly.io](https://fly.io/), in particular, and their use of [FLAME](https://fly.io/blog/rethinking-serverless-with-flame/) are very exciting (relatively) recent developments.

On top of this, there are numerous high-quality learning resources developed by core contributors and often even the creators of these languages ranging from learning the languages to learning about their important libraries, designing systems that scale, metaprogramming, and more. The community that has built up around the BEAM is full of experts and a relative wealth of friendliness and dearth of hostility. That being said, if that weren't the case I don't feel it would diminish the value of the technology - it's just a pleasant addition to an already overwhelming number of reasons to appreciate it.

### BEAM Languages

Thus far, I've spoken almost entirely about the virtual machine itself and not about the languages which compile to BEAM bytecode. This is because the the virtual machine really is the **most** important part, but it is not the **only** important part. Luckily, if you're a picky programmer with a preference for particular syntax, there are mutliple viable languages to choose from.

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

If you _do not_ burst into flame in the vicinity of S-expressions and enjoy working with a lisp, there's _[Lisp-Flavoured Erlang](https://lfe.io/)_:

```lisp
(defun (hello_world)
  (io:format "Hello world!~n"))
```

For people who can't give up their C-style braces or feel that they need static typing, there's also _[Gleam](https://gleam.run/)_ which layers Rust's syntax onto SML/OCaml/F#'s semantics (bar currying-by-default) and the BEAM's execution model:

```rust
fn hello_world() {
  "Hello world!" |> io.println()
}
```

The growth of any of these languages benefits the others due to the interoperability afforded by their shared virtual machine. The most obvious example here being the fact that all of these languages utilise the Erlang Open Telecom Platform as the basis of their concurrency systems.

## Reaching New Heights

Although some familiarity with Erlang is beneficial no matter which language you choose to use (it is the _Erlang_ Abstract Machine, after all), I feel that, upon inspection, Elixir is the clear frontrunner for potential growth and utility over the next decade.

There are several very exciting developments going on in the Elixir ecosystem, from StackOverflow's most-loved web framework for two consecutive years, [Phoenix](https://www.phoenixframework.org/), to the numerical computing project [Nx](https://github.com/elixir-nx) which is rapidly growing the presence of the language in the machine learning and data science space. Nx also includes the amazing [Livebook](https://livebook.dev/), which is something of an analogue to Jupyter Notebook. [Nerves](https://nerves-project.org/) is the final community project that I'll mention here - a framework for creating software for embedded devices. This is exciting for those of us who are usually confined entirely to writing to web services or command-line tools but would like to have a familiar environment with which we can learn about embedded programming.

There has been a lot of work done by José Valim, Giuseppe Castagna, and Guillaume Duboc in recent years to develop a gradual type system for Elixir, which has resulted in new research on [Set-Theoretic Gradual Types](https://arxiv.org/abs/2306.06391). This has already begun its integration into the Elixir ecosystem, and I believe will serve to improve adoption by programmers who categorically refuse to use dynamically typed languages (beyond the actual concrete value proposition of opt-in compile-time type checking eliminating certain types of errors).

## Do Not Look Down

The adage that there is _"No silver bullet"_ is perhaps second in frequency only to variations of object-oriented programming (in the C++ tradition) sloganeering about **SOLID** principles or **DRY** or what-have-you. And it is, of course, true that we have no tools which solve _every_ problem. In fact, we have many tools which solve no problem at all. But Erlang was created to solve a _particular_ problem: distributed programming. As it so happens, most programming today involves distributed systems.

It turns out that you can squeeze a lot of performance and faux-simplicity from programs that ignore the benefits of distributed programming, much like making simplifying assumptions aids the clarity and conciseness of scientific or mathematical proofs (at the expense of correctness and comprehensiveness). Sometimes this is an acceptable, or (much more rarely) necessary exchange.

Instead of leveraging the BEAM, though, we default to bolting its features onto our programs with disparate tools that require generous application of duct-tape-YAML to keep the plumbing from leaking sewage onto our floors.

### It's All About Popular

Fashion has been an ever-fickle guiding hand of programming history since its inception, with just as much power as any meritocratic assessment of technology, if not more. One trade-off of BEAM languages is that by comparison to other programming language communities like Python, JavaScript, and so on, the ecosystem is rather small. It's not terribly small, though - you'd have an easier time finding an Elixir programmer than a [Janet](https://janet-lang.org/) programmer to employ. The oft-cited "friendly syntax" of Elixir goes a long way in onboarder-enthusiasm and there is even an [entire book](https://pragprog.com/titles/tvmelixir/adopting-elixir/) on the process of adopting the language and onboarding teams.

With the consistent growth Elixir is experiencing and the large existing footprint Erlang has in the industry, I don't feel that this concern holds up to much scrutiny unless you believe that your coworkers or employees are utterly incapable of learning new things. If that _is_ the case, I recommend finding a new job or hiring new employees.

### Soft-Real-Time

Another trade-off made when working with the BEAM is that it aims to achieve "soft-real-time" performance. It's not suited to real-time programs the way Rust is, for example. There is overhead to its runtime behaviour and the garbage collection mechanism. Because much of this overhead is designed to tolerate large-scale systems, there is an efficiency loss in scaling down to single-threaded environments where other garbage-collected languages will outperform Elixir or Erlang in many kinds of programs. I shudder to imagine the conclusions drawn from comparing LeetCode performance benchmarks between Elixir and JavaScript.

The cost-benefit analysis becomes less grim when considering that, generally, performance constraints on the kinds of single-threaded, synchronous programs written in high-level languages are effectively inconsequential. If we can glue our operating systems together with Python, there's certainly no need to fear the performance of Elixir in these contexts.

Additionally, in the domain these languages are designed for, they look far more appealing next to their competitors. Benchmarks in general are difficult to run well, and even more difficult to trust. That said, if you've the time and curiosity, [this article](https://www.erlang-solutions.com/blog/comparing-elixir-vs-java/) demonstrates the broad comparison of a BEAM language against a non-BEAM language in a context that is relevant (network-bound, mixed-workload, concurrent systems). In time I imagine that the [aforementioned decline](#finding-footholds) of Koomey's Law will play a role in seeing languages which parallelise processes more easily become more performant in ways others can't.

## Summit

If you'll excuse the irony of closing with a variation on an aphorism after the smug first paragraph of the [previous section](#do-not-look-down), one might say that ["Every sufficiently complicated distributed program contains an ad hoc, informally-specified, bug-ridden, slow implementation of half of the BEAM."](https://en.wikipedia.org/wiki/Greenspun%27s_tenth_rule)
