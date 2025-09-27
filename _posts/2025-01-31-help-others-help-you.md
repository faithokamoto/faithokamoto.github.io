---
layout: post
title: Help others help you
subtitle: January 2025
tags: [published-code-critique, documentation, naming]
author: Faith Okamoto
---

Technically this paper isn't published yet, but it's on [biorXiv][Preprint]
and has gone through revision with a journal, so I'm using it. Also I've just 
spent the better part of a week trying to use its software. 

This month's paper:
Walia S *et al.*. Compressive Pangenomics Using Mutation-Annotated Networks.
*bioRxiv* 2024. doi: [10.1101/2024.07.02.601807][Preprint]

## Original code

This is a marker paper for a software tool. The tool, `panmanUtils` (which works
with the novel PanMAN data structure) is on [GitHub][TheirCode]. The authors
"welcome contributions from the community". My current rotation project is to
extend `panmanUtils` with more functionality ([GitHub][MyCode]), so I guess I'm
the community.

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Keep your documentation up to date

I'll be approaching this critique from the perspective of someone who wants to
improve/extend `panmanUtils`. They'll have been excited by the [paper][Preprint]
and want to get their hands dirty with this cool new data structure. Step one
would be to read the availabe documentation.

Unfortunately for this hypothetical person, that's sort of the exact wrong move.
The [README][README], as far as I can tell, is largely fine, if incomplete. That
would be fine. The repository links to an external [wiki][Wiki] with more
details. However, that wiki is riddled with enough errors that it's hard to know
what to trust.

A few examples:
* Multiple commands which use files in the `test/` directory are included as
examples. Several of these commands use files which do not exist in `test/`.
* At least one option (`--fasta`) has a different description in the wiki vs.
by the tool itself (when running `--help`). The wiki's description is incorrect.
* Copy-paste errors, e.g. two options in Table 1 with the same description.
* Numerous small English grammar errors.

Users should be able to trust documentation as they start on the steep learning
curve of figuring out how the code-base works. When that trust is violated, what
is there left to rely on? Reading the code? Well, that brings me to the next
issue...

### Explain what functions do, *especially similar ones*

If you don't have time for [docstrings][DocstringsTag], at least throw a brief
comment defining what a function does. This goes double if there are multiple
similar functions. The user wants to know which they should use. If there are
subtle differences, then explain what they are and why they exist.

An example are the functions in [fitchSankoff.cpp][FitchSankoff] (in order):
* `nucFitchForwardPassOpt()`
* `nucFitchForwardPass()`
* `nucFitchBackwardPassOpt()`
* `nucFitchBackwardPass()`
* `nucFitchAssignMutations()`
* `nucFitchAssignMutationsOpt()`
* `blockFitchForwardPassNew()`
* `blockFitchBackwardPassNew()`
* `blockFitchAssignMutationsNew()`
* `nucSankoffForwardPassOpt()`
* `nucSankoffForwardPass()`
* `nucSankoffBackwardPass()`
* `nucSankoffBackwardPassOpt()`
* `nucSankoffAssignMutationsOpt()`
* `nucSankoffAssignMutations()`
* `blockSankoffForwardPass()`
* `blockSankoffBackwardPass()`
* `blockSankoffAssignMutations()`

Some of the differences are intuitive. `Fitch` functions use the algorithm from 
[Fitch 1971][Fitch1971], and the `Sankoff` ones [Sankoff 1975][Sankoff1975].
Some of these functions work with mutations of "blocks" (a concept defined in
the paper) and some of them work with nucleotides.

But what does it mean if `New()` or `Opt()` are appended to a normal function
name? Which of these functions should I use, if I want to have the Fitch
algorithm as a subroutine? If I want to build something similar to the Fitch
algorithm, which should I emulate?

These functions are not user-facing, but anyone trying to develop around them
will have a headache. If e.g. the `Opt()` versions are experimental and under
active development, then perhaps at least put a comment in the `.hpp` file to
warn about that.

This problem is multiplied over all the many functions which work together to
create the complete tool. Untangling that web would be much easier if each part
were labeled.

----

Eventually I figured out what was happening, via liberal use of external
references and staring at nothing. If it wasn't my project, I might've given up.
You will lose potential contributors if the barrier to entry is too high. Ease
their way in, please. Signpost hat's already there and how it can be used.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[CV]: https://faithokamoto.github.io/cv/
[DocstringsTag]: https://faithokamoto.github.io/tags/#docstrings
[Fitch1971]: https://doi.org/10.2307/2412116
[FitchSankoff]: https://github.com/TurakhiaLab/panman/blob/main/src/fitchSankoff.cpp
[MyCode]: https://github.com/faithokamoto/panman
[Preprint]: https://doi.org/10.1101/2024.07.02.601807
[README]: https://github.com/TurakhiaLab/panman/blob/main/README.md
[Sankoff1975]: https://doi.org/10.1137/0128004
[TheirCode]: https://github.com/TurakhiaLab/panman
[Wiki]: https://turakhia.ucsd.edu/panman/