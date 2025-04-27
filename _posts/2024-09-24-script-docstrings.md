---
layout: post
title: Script docstrings
subtitle: What is this file, and why should I care?
tags: [file-level, docstrings]
author: Faith Okamoto
---

I advocate providing [docstrings][PEP257] for scripts/modules/[whatever you call
a code file]. In addition to describing the file in the [README][README], by the
way. Important information should be in multiple places.

## What's a script docstring?

Forgive me, my terminology is rather Python-infected, since I learned about
docstrings through [PEP 257][PEP257].

A script docstring is a **succinct description of a script**, appearing at the
top. In Python, it would be a string literal, e.g.

```python
"""Helper for genotype processing.

Provides functions and constants to standardize genotype I/O.

CONSTANTS
- `ALLOWED_CHR_NAMES`: list of valid chromosome strings
- [more constants]

FUNCTIONS
- `filter_maf()`: filter genotypes by minor allele frequency
- [more functions]
"""
```

My "docstrings" for bash scripts look different, and technically occur second,
after the shebang:

```bash
#!/bin/bash
# Submit GWAS batch jobs by chromosome/trait
# Parameters: <# of autosomes> <directory with trait files>
# Example: bash code/submit_gwas.sh 20 data/phenotypes
```

There are many possible formats. The reader should quickly know the essentials:
- What is this script's purpose?
- How do I use it?

## Why are script docstrings needed?

First and foremost, script *doc*strings are *doc*umentation. I repeat: write
documentation both other people and yourself in a few months. Imagine you were
playing around with some code and then shelved it for later. When you pick it
back up, you want to jump right back into using it, not spend half an hour
figuring out how to invoke your script correctly.

Such docstrings are also a useful reference for yourself *as you develop* the
code. In my first example, a centralized list of all of the module's exports is
quite useful. I can scan it quickly and then decide what to use. Or, as in the
second example, the ready-made example invocation is easy to copy-paste and then
modify as necessary. This is why I continuously update my script docstrings as
the script they document itself changes.

But why do you need *script* docstrings, instead of just docstrings for the
individual components? The answer is that script docstrings are standardized
and accessible across all scripts. It can be a significant time investment to go
trawling through a large script. Having a docstring up top immediately tells the
reader if that investment is useful. If it is useful, then it tells them which
parts to beeline for.

I wrote this post because I would love for more code to have these docstrings.
Hopefully I've now convinced you of their utility.

[PEP257]: https://peps.python.org/pep-0257/
[README]: https://www.makeareadme.com/