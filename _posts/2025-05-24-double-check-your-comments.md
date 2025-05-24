---
layout: post
title: Double-check your comments
subtitle: May 2025
tags: [published-code-critique, comments, last-pass]
author: Faith Okamoto
---

I usually critique biology/bioinformatics papers (since that's my field). This
month, we're looking at a paper where I do not understand any of the jargon.

This month's paper: Cheng HW *et al.* A retrograde planet in a tight binary star
system with a white dwarf. *Nature* 2025. doi: [10.1038/s41586-025-09006-x][DOI]

## Original code

This paper's code is on [GitHub][Code]. Its structure is simple, according to 
the [README][README]. A few dependencies and one main script to run. I'll be
focusing on that script: [`compute_bse_nest.py`][Script].

## Critique

My first critique post was also focused on [doing a final clean-up][Cleanup].
This time I'll just deal with the use of comments in code released to others.

### If a line isn't used, remove it

This isn't a great first impression:

```python
#!/usr/bin/python
import numpy as np
import os, sys
import matplotlib
#mpl.use('Agg')

matplotlib.use('Agg')
```

Reading between the lines, `matplotlib` used to be imported `as mpl`. Now,
`#mpl.use('Agg')` is redundant. It's literally not run, and it wouldn't work.

Such irrelevant lines are best removed. As in deleted, not just commented out.
This simplification means others will only see the code you actually ran. That's 
the point of code release, right? To show others the code that got the results. 
So only leave the parts that were run.

### Typo-check, folks

One of the section headers is

> innitial guess of parametrs to vary

Needless to say, there are multiple typos here. Section headers are mean to be
easily understandable markers. Plus, it's a header. It pops out of the screen.
These typos are unprofessional. While professional scientists aren't usually 
professional programmers, code should be presentable when it's presented.

### Old parameters aren't needed

```python
#par    = np.array([2.3, 1.4, 2500.0, 0.8, 10000.0]) # init_M1, init_M2, init_P, init_e, init_Bw (used for optimisation)
par    = np.array([2.4, 1.4, 750.0, 0.8, 16000.0]) # init_M1, init_M2, init_P, init_e, init_Bw (used for optimisation)
```

These parameters clearly went through iterations. The second line is run. The 
first line is, I guess, an old version.

During active development it can be useful to keep previous versions to refer
back to. But, when a script is released, the only reason to include old versions 
would be to explain why/how they were changed. We don't have that context here.

----

Those are the main categories of comment-related issues I see with this code.
There are many other problems as well: poor spacing, inconsistent naming, lack
of docstrings, etc. but I can't critique every detail or I'd be here all day.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Cleanup]: https://faithokamoto.github.io/2024-12-23-do-a-final-cleanup/
[Code]: https://github.com/3fon3fonov/BSE_NestSamp
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1038/s41586-025-09006-x
[README]: https://github.com/3fon3fonov/BSE_NestSamp/blob/main/README.md
[Script]: https://github.com/3fon3fonov/BSE_NestSamp/blob/main/compute_bse_nest.py