+++
title       = "What's in a Function Signature?"
date        = 2025-05-04
description = """
Function signatures are the boundaries of the layers of abstraction in software. They are one of the most frequently interacted-with parts of a code base, as any developer uses them as the first port of call when interacting with a new module.
"""
[taxonomies]
tags = ["rust", "javascript", "typescript"]
+++

## The Dotted Line

A function (or method) signature, [according to MDN Web
Docs](https://developer.mozilla.org/en-US/docs/Glossary/Signature/Function),
“defines input and output” of a function or method. It can include
parameters, return values, types for said paramters and return values,
possible exceptions or errors, and accessiblity information (i.e. in
what scope(s) the function can be accessed). Most languages meet this
definition with some combination of these features; some languages have
additional features as well.

Developers might intuitively understand a function signature as “the
first line of the function, which defines the contract by which it can
be invoked”. This latter understanding is important because the concept
of a “contract” implies something about *the role the function signature
plays in software design and development*.

To demonstrate this, we will work through multiple iterations of a
function signature across 3 programming languages. Each iteration will
provide more information, or alter the way the information is presented,
with the intention of expressing as much useful information to the
reader as possible about a function without needing to see its
implementation.

### Jarring Javascript

We’ll start with a very simple (almost certainly **too** simple)
Javascript function signature. For our purposes, the implementation is
irrelevant.

``` javascript
function c(p, n) {}
```

What can we learn about this function based on this line alone? Not
much. It’s a function that takes two arguments. The language is dynamic,
so we don’t know the types of data it accepts. Perhaps `p` has some
significance to the kind of parameter it is. A [P
value](https://en.wikipedia.org/wiki/P-value)? A probability? `n`
usually represents a number, so that’s probably what we should pass in
there. Well, there’s little use in blind guessing, let’s move on to the
next iteration and see what else a function signature can convey.

``` javascript
function changeName(person, name) {}
```

Ah! `changeName`. Looks like our initial assessment was quite far off.
This is a simple function that takes in a `person` (presumably an object
of some kind), and a `name` (presumably a string or something that can
be turned into a string), and then changes the name of the person to be
the provided name. But, wait, what does it mean to “change the name of
the person”? Do we mutate the value directly on the object we pass in?
Or do we get a new `person` with the changed name? If it’s mutating the
state of its parameter, that could cause a lot of complications or
unexpected bugs. Let’s take a look at the next version and find out.

``` javascript
/**
 * Changes the name of a person.
 *
 * @param {Object} person - The person whose name will be changed.
 * @param {string} name - The new name to assign to the person.
 * @throws {TypeError} if the input types are invalid.
 * @throws {Error} if the name is empty.
 */
function changeName(person, name) {}
```

Okay, maybe we’re stretching the definition of a function signature here
a little bit. All we’ve done is add a
[JSDoc](https://jsdoc.app/about-getting-started) comment! The actual
signature remains the same. However, with this change, a developer can
inspect the function and get a nice description with all of these
additional details in their editor. On top of that, there are editor
extensions that will do static analysis based on this information to
perform a limited kind of type checking. JSDoc’s primary utility is
actually in generating documentation directly from Javascript source
code. What information do we get for the additional effort? Well, for
one, we now get a natural language description of the function’s
purpose. We also know more concretely the types of the parameters it
accepts.

The author could also have provided documentation on the return type,
but there isn’t any. Maybe they forgot. Or maybe it mutates the input
and so there is no return to document. That’s not something we can
conclude without running the function, or checking its implementation. A
new piece of information has been surfaced though! This function can
throw errors! Multiple kinds of errors, in multiple possible scenarios.
If the caller didn’t know about this in previous iterations, they could
have gone unhandled in user code until an unexpected error was thrown at
runtime, after which it would need to be investigated, which would
potentially involve jumping into the implementation of this function to
understand what was causing the error.

So, we’ve improved significantly on the initial Javascript function
signature but there are still many uncertainties. What benefit can we
get by grafting gradual types and a build step to the language?

### Typical Typescript

With Typescript, we get a build step with a transpiler that will perform
some correctness checks on our function calls. We can then move our type
information directly into the type system, and prevent invalid function
calls by having them fail the build. This approach brings many of the
same benefits of just documentation, like static analysis tools and
editor extensions.

``` typescript
/**
 * Changes the name of a person.
 *
 * @throws {TypeError} if the input types are invalid.
 * @throws {Error} if the name is empty.
 */
function changeName(person: Person, name: String) {}
```

Unfortunately, Typescript’s error model is not integrated into its type
system, and so we still need to document possible errors. The JSDoc
syntax has been used here for consistency, though JSDoc + Typescript is
not a popular combination. Most often, developers opt for the benefits
of gradual typing and bite the bullet on untracked errors, abandoning
the other benefits of a tool like JSDoc (there is a tool called
[TSDoc](https://tsdoc.org/) but it is infinitesimally unpopular by
comparison to Typescript itself).

This time, the lack of return is less ambiguous than before. We know
that this function doesn’t return anything! So, it must mutate the input
parameter `person` to actually change its name.

Assuming it passes its unit tests.

Assuming those unit tests are correct.

Assuming it **has** unit tests.

Well, domain and logic errors aren’t the concern of the language,
anyway - that’s a problem even the most fully-featured compilers can’t
solve. Let’s move on to a slightly different version of this function
signature that presents a slightly *different* problem.

``` typescript
/**
 * Changes the name of a person.
 *
 * @throws {TypeError} if the input types are invalid.
 * @throws {Error} if the name is empty.
 */
function changeName(person: Person, name: String): Person {}
```

This function signature shows that it returns a `Person` object, so it
probably doesn’t mutate the input. It’s not a guarantee, though, since
it could technically mutate it and then return it for convenience in
chaining functions… Maybe this is something that could have been
clarified in the description — as useful as documentation is, it’s
dependent on the author and their ability to communicate design intent
in natural language. That’s not something that can be checked by a
compiler or static analysis tool.

At this point, we’ve hit the boundaries of most popular languages’
function signatures. There are nuances such as Go’s ability to implement
a function on a data type for dot-notation, but really that’s just
changing the calling convention. Perhaps the main thing that hasn’t been
covered yet is how languages handle passing arguments by reference and
value. This is a language-dependent concern, but it’s very important for
understanding certain characteristics of your functions. For example, if
we knew that our `person` argument was being passed by value, and not by
reference, then we could be certain it wasn’t being mutated in the
function. In Javascript, objects are passed by reference (as are most
heap-allocated data types in most languages). In Go, or C, among many
other languages, we can explicitly pass pointers to functions. This
allows more fine-grained expression of intent in our function
signatures.

### Relentless Rust

If we have control over pass-by-reference and pass-by-value in multiple
languages, why specifically use Rust as our final language? Well, Rust’s
references have additional semantic meaning that communicate more
information than other languages. We’ll see the benefits of this soon —
for now let’s take a look at the first version of our function signature
in Rust:

``` rust
/// Changes the name of a person.
fn change_name(person: Person, name: String) -> Person {}
```

For the most part, this looks near-identical to the previous Typescript
signature. In fact, although we’re providing a summary documentation
comment, we’ve done away with the error documentation, so it seems like
there’s *less* information here, at first glance. This is not the case;
Rust doesn’t have errors or exceptions in the way many other languages
do . If the return type doesn’t show us there can be an error, then
there won’t be. If the possibility of failure exists, we can track it in
the type system, as we can see in the next iteration.

``` rust
/// Changes the name of a person.
fn change_name(person: Person, name: String)
    -> Result<Person, NameError> {}
```

This version returns a `Result` type. Not only does it tell us the type
it can return on success, but we can also provide a specific error type,
customised to have direct meaning within our domain. The caller of this
function is forced by the compiler to handle both the good and bad
execution paths, and they’re aware of the possible failures *before they
even call the function*. This information being integrated into the type
system, combined with quality static analysis and editor integration,
mean that all of this information can be seamlessly leveraged to
streamline the developer’s use of the code.

But there is another piece of information in this signature that hasn’t
been covered yet: it tells us how the arguments are being passed. In
Rust, when a function accepts a plain type as an argument, the memory
that stores that parameter is moved into the function’s scope when it is
called. We literally *move* the argument into the function,
relinquishing that memory from the calling scope into the function
scope. We only get it back if the function returns it to us. Otherwise,
it gets cleaned up when the function completes. We can also pass by
reference, of course:

``` rust
/// Changes the name of a person.
fn change_name(person: &Person, name: &str)
    -> Result<Person, NameError> {}
```

This version of the function signature accepts its arguments by *shared
reference*. This means that the reference can be borrowed by multiple
functions, and the type checker guarantees certain kinds of safety by
allowing them to *access* the data but **not** allowing them to *modify*
it. Based on this, when we see a parameter passed by shared reference to
a function, we know it **cannot** be mutated in the function. And
because of how the references work in Rust’s type system, there’s no
possibility of unforeseen [shallow copying
issues](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)
that you might run into in a language where a seemingly immutable
reference is passed, and although the reference can’t be changed, values
accessible transitively through it can be.

Whether for performance constraints or due to the nature of the domain
we’re working in, some problems need to be solved with mutation,
however. So, how does Rust handle mutation?

``` rust
/// Changes the name of a person.
fn change_name(person: &mut Person, name: &str)
    -> Result<Ok, NameError> {}
```

Looking at the final iteration of `change_name` above, we can see that
`person` is passed with a *mutable reference*, also called a *unique
reference* because it cannot be shared across multiple callers. With
this signature, we can see that the function needs to take in the
argument with permission from the type checker to mutate it, it can
change the name, and then it returns a result showing whether the
function succeeded to make the change, or ran into an error. It’s
extremely clear from just the signature what this function does.

### Fill in the Blank

By comparison, let’s take a look at two of the earlier versions of this
function signature. First, in Javascript:

``` javascript
function getDeliveryRoute(packages, options) {}
```

Let’s ask ourselves a few questions about this version.

#### 1.  What does it do?

Assuming based on its name, this function gets a delivery route for some
packages, and accepts some options which may alter the kind of route it
determines. This is a tenuously acceptable answer.

#### 2.  What types does it accept for its arguments?

There is no way of knowing the exact types. Because the language is
dynamic, any type will do, so long as it has the properties needed for
the implementation of the function… which we can only know by inspecting
the implementation. Not a good answer.

#### 3.  What does it return?

Ideally, it returns a delivery route. We know nothing about what kind of
data that might be. No good here, either.

#### 4.  What kind of errors or exceptions can occur?

There is no way of knowing without writing a test or debugging it, but
we’re supposed to be consuming this code and not checking its
implementation. It’s not doing us any favours.

#### 5.  Does it run at all?

As with the previous question, we really don’t know.

#### 6.  Is it publicly accessible?

Presumably not, as there’s no `export` keyword but, in Javascript,
module members can be exported in a separate statement. So, maybe.

#### 7.  Are the parameters passed by reference or by value?

That depends on what gets passed in. If they’re certain primitive types,
they’ll be passed by value. If they’re most types, they’ll be passed by
reference.

#### 8.  Does it mutate its parameters, affecting external state?

Absolutely no idea.

<br />

------------------------------------------------------------------------

<br />

After our journey through increasingly descriptive function signatures,
that last one really shows its deficiencies. There are absolutely
benefits to dynamic types, and much could be done to improve this with
some good, in-source documentation. But for the purposes of
demonstration, let’s consider the same questions for the more
disciplined Typescript signature below.

``` typescript
/**
 * Determines a delivery route for a set of packages considering
 * distance, time constraints, and delivery priorities.
 *
 * @throws {PackageDataError} if any package is missing required
 * coordinates or timeframes.
 * @throws {RouteError} if no viable route can be calculated with
 * the given constraints.
 * @throws {TypeError} if either parameter is not of the correct
 * type at run time.
 */
export function getDeliveryRoute(
  packages: List<Package>,
  name: DeliveryOptions
): Route {}
```

#### 1.  What does it do?

This time, we have a nice summary that gives a good understanding of its
behaviour. It gets a delivery route for a set of packages and considers
distance, time, and some set of domain-related priorities. This is a
great improvement.

#### 2.  What types does it accept for its arguments?

We can see that it accepts a `List<Package>` and a `DeliveryOptions`,
both of which are models relating to the domain and can be easily
inspected for their properties. Another valuable improvement for the
caller of this function.

#### 3.  What does it return?

Now we have confirmation that it returns something, and that something
is a `Route` whose properties are knowable when calling the function,
without checking the function itself.

#### 4.  What kind of errors or exceptions can occur?

As far as the documentation tells us, there are a few kinds of errors
related to the domain, and a possible typing error due to edge cases
with gradual typing. It’s a step up from before, but it’s also easy to
miss niche error cases when documenting them this way.

#### 5.  Does it run at all?

For the same reasons as the Javascript version, we unfortunately have to
answer ‘maybe’.

#### 6.  Is it publicly accessible?

This time, the implementer has opted to place the export in the function
signature line, so we can definitively say yes.

#### 7.  Are the parameters passed by reference or by value?

Now that we know they are `Object`s of some kind, they will be passed by
reference. Assuming nobody does any funny business with the type
checking and passes in illegal parameters. All this would do is throw an
error, but still, it’s not a *true* guarantee.

#### 8.  Does it mutate its parameters, affecting external state?

Based on the return and the description, it’s unlikely. We can’t be
certain, though.

<br />

------------------------------------------------------------------------

<br />

Overall, this signature has provided a wealth of new information and
many more guarantees. It would be much easier for a caller of this
function to understand its characteristics than before. But there are
rough edges and some facets of the signature that require good behaviour
from the developer to be documented. We know that much of this can be
moved into the type system in Rust, and so in our final iteration, we’ll
take a look at a full-featured signature with not only a documentation
comment, but also an executable example of the function call and
additional explanation of the possible error values.

```` rust
/// Determines a delivery route for a set of packages considering
/// distance, time constraints, and delivery priorities.
///
/// # Examples
///
/// ```
/// let test_package = Package {
///     Sku: 123,
///     Name: "Test Package",
///     Weight: 12.as_g()
/// };
/// let packages = vec![Package::new()];
/// let options = DeliveryOptions::default()
///     .with_algorithm(Algorithm::DistanceFirst);
/// let route = get_delivery_route(&packages, &options)?;
///
/// assert!(route.total_distance() < 100.0);
/// ```
///
/// # Errors
///
/// Returns `RouteError::InvalidPackageData` if any package is
/// missing required coordinates or timeframes.
///
/// Returns `RouteError::NoViableRoute` if no viable route can
/// be calculated with the given constraints.
pub fn get_delivery_route(
    packages: &[Package], 
    options: &DeliveryOptions
) -> Result<Route, RouteError> {}
````

#### 1.  What does it do?

We have the same useful description as before, but now we even get to
see an example of it being called so we can place it in context and see
some of the assiciated data types we may want to pass in (such as
`DeliveryOptions` having an `Algorithm` enum).

#### 2.  What types does it accept for its arguments?

As with the Typescript signature, we can see the exact types it accepts
right there in the signature. Shared references to a collection of
`Package`s and a `DeliveryOptions`.

#### 3.  What does it return?

This time, the return type contains our error information as well as the
type it returns on success. The `Route` type is either a struct or enum
of some kind which will specify the data available to the caller of the
function. Our success case is about equivalent to the Typescript
signature.

#### 4.  What kind of errors or exceptions can occur?

Not only do we know that it *can* fail, we have an enum of error values
that it could provide as a result, and if it does we can handle each
however we like. The documentation even explains what causes each of the
possible errors to occur. And due to the language’s error model, we know
that no other error type will occur (unless someone applies blunt force
trauma to the CPU, but we only expect that kind of resilience from
Erlang).

#### 5.  Does it run at all?

Although it’s never a guarantee that this kind of thing will be
provided, it **is** a prominent pattern in the Rust community to include
example code snippets with assertions above a function signature. So
much so that many editors allow you to execute Rust code snippets from
within the source code, sometimes even just from hovering a function
invocation and inspecting the popup. So, without writing any tests,
running the application, doing any direct debugging, we do have a
straightforward way to see that it behaves as expected.

#### 6.  Is it publicly accessible?

Yes! The `pub` keyword is the way to make a module member publically
accessible, and it must be part of the function signature to apply.

#### 7.  Are the parameters passed by reference or by value?

The signature clearly shows that they are passed by reference. Not just
any reference, a shared reference. We know not just the way their memory
is handled, but how/whether they can be passed to other functions at the
same time. If we know that the types themselves (`Package` and
`DeliveryOptions`) are thread-safe, then we even know that the shared
references are thread-safe. To contrast, even if the underlying types
were thread-safe, `&mut` parameters are **not** thread-safe.

#### 8.  Does it mutate its parameters, affecting external state?

Because the arguments are not passed mutably, the function signature
guarantees that the parameters will not be mutated and the function will
not affect external state.

<br />

------------------------------------------------------------------------

<br />

All of these answers are knowable by reading just the function
signature, checkable at compile time, and the documentation comments
surface information in your code editor so you can understand all of
this as a user of the function, without needing to inspect the code
itself. Even without the extensive doc comments, we still know about
mutation, input/output types, possible errors, module accessibility, and
even thread safety & data race information.

### So, Really, What’s in a Function Signature?

I’ll answer a question with a question: How much useful information can
you fit in it?
