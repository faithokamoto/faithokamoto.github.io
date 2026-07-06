---
layout: post
title: Filenames matter
subtitle: so what does this do?
tags: [published-code-critique, file-level]
author: Faith Okamoto
---

I saw that Li has another "mini" tool, so I though I'd look, as I did with
[minimap2][Minimap2Blog]. Also, it's the literal last day of the month. Being on
vacation does that to ya.

This month's paper: Li H and Homer N. Fast genomic read alignment with minibwa.
*arXiv* 2026. doi: [10.48550/arXiv.2606.15357][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

I have basically one main grip with this code, and it's late, so I'm just going
to put it in a little center section. The filenames for this project are
incredibly inscrutable. What does `mbpriv.h` do? `pe.c`? If I'm trying to
navigate this to find the bit of algorithm that's relevant to me, where do I
look? (Clicking in to the files doesn't help either; things are over-briefly
named in general, and there aren't good [docstrings][DocstringsTag] for anything
including the file in general.)

The README doesn't provide pointers for what goes in what files. The files
themselves don't provide help either. Usually I can at least go by names
(e.g. a file called `readfilter.hpp` is probably about filtering reads). But
abbreviations that only make sense to the maintainers? Those are inscrutable to
people trying to learn.

Brilliant tool and algorithms, I'm sure. I just can't understand the code. And I
can't even navigate via filenames.

----

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/lh3/minibwa
[CV]: https://faithokamoto.github.io/cv/
[DocstringsTag]: https://faithokamoto.github.io/tags/#docstrings
[DOI]: https://doi.org/10.48550/arXiv.2606.15357
[Minimap2Blog]: https://faithokamoto.github.io/2025-12-13-understanding-an-api/