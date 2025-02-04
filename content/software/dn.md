+++
title = "dn"
description = """
A note-taking, file-organisation, and personal knowledge management system
utility for cross-platform terminal use.
"""
date  = 2024-12-21
+++

## Overview

`dn` is a CLI tool for creating and renaming files with a regular structure. The benefit of this regular structure is that it is predictable and compatible with regular expressions. An example file name with every possible segment present looks like this:

```txt
20241221T132030==1a--example-file__test_demo.md
```

It has a mandatory unique identifier and file extension, with optional the optional segments for signature, title, and keywords. The purpose of identifier, file extension, and title are most likely self-evident but the benefit of keywords is that different files can be searched and grouped by subject-matter or theme, and the signature allows for organising files according to an additional arbitrary user relationship. This means that `dn` can be used to implement a digitial [Zettelkasten](https://zettelkasten.de/overview/) with [Folgezettel](https://zettelkasten.de/folgezettel/) if a user wants to.

```sh
# Make a new note.
dn new --title foo --keywords example --extension dj
```

Because of the naming scheme's regularity, many other shell tools like [ripgrep](https://github.com/BurntSushi/ripgrep) and [fzf](https://junegunn.github.io/fzf/) can be used to build a personalised note-taking or file-organisation workflow.

```sh
# Search notes directory for files with fzf 
# and open the chosen file in neovim.
rg $DN_DIRECTORY --files | fzf | xargs hx
```

## Features

- Flexible creation and renaming of files
- Front matter generation
- Template insertion
- Configurability via a single TOML file
- Extensibility with text editor plugins
- Unicode-aware sorting of keywords
- Shell-completion scripts
- Manpages

## Insights

The initial motivation for this project was to have a convenient, small, portable solution for managing my personal notes. It provided an opportunity to learn a lot more about Rust, and about the intricacies of creating open source software. I was able to collaborate closely with another maintainer, ensure compliance with the FSFE's [REUSE](https://reuse.software/) standard, and write extensive documentation both in-source and outside.

Many things have been learned along the way:

- The benefit of good in-source documentation facilities
- Regular expressions are not as opaque as I thought
- Rust's memory model is actually quite intuitive and helpful
- Copyright and licensing concerns are very important in open source work
- Dependencies are hard to avoid
- Implementation without design leads to confusion and mess

The language and libraries chosen for this project were borne of convenience and utility rather than personal preference. I needed a language which had proper UTF-8 support with powerful text manipulation features, and the ability to compile to a single binary for all major personal computing platforms. Rust was the most appropriate choice for this use case. It was an explicit goal from the beginning to keep dependencies minimal, and that will remain the case until `dn` is considered finished at which time all dependencies will be vendored and maintained with the tool itself.

## Source Code

The source code for `dn` is hosted on GitHub and can be found [here](https://github.com/mmibbetson/dn).
