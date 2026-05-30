---
layout: post
title: Releasing code without data
subtitle: for legal reasons
tags: [published-code-critique, runnable, examples]
author: Faith Okamoto
---

For those readers who care about the ongoing "Faith loves *Project Hail Mary*"
storyline, I've now watched it five times :D

As for the critique, I didn't have a paper relevant to work to pull, so I went
looking around *Nature*. I found this interesting one where they released code
but not the underlying data. 

This month's paper: Ghai S *et al*. Technology mediation in child sexual 
exploitation and abuse in Africa and Asia. *Nature* 2026. doi:
[10.1038/s41586-026-10525-4][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

### What's important is the explanation

Usually published papers also release underlying data. This one didn't:

> **A demo dataset is not available.** The data used in this study involve
> sensitive child-level responses collected under a restricted access agreement
> with UNICEF and cannot be shared publicly. We considered generating synthetic
> data but determined this could risk misuse or misinterpretation given the
> sensitivity and complexity of the variables.
>
> **In lieu of a runnable demo, all scripts have been rendered to HTML outputs**
> (available in the repository root) that show every line of code alongside all
> results, figures, and model diagnostics.

While of course data is nice, it can't always be public. Another example I've 
seen is proprietary company data. For a paper that can't release data, this 
disclaimer is really the next best thing. It briefly explains both why there is 
no data and what they've done to mitigate that. 

### Describing methods in detail

Okay, so we can't see the data. Can we at least understand what was done to it?
Yes, yes we can! There is a lovely list of files along with an explanation of
what each does. The hardware and software used to run this code? In the README.
Pipeline order? In the README, and with files labeled by step. It's beautiful <3

Regular readers of [my critiques][CritiqueTag] would know that I often complain
about not knowing what anything is doing or what dependencies were used.
Hilariously, this paper, where it's impossible to run the code, is getting an A+
from me on code documentation.

Of course, that documentation is especially important when the reader can't test
the code for themself. By going into plenty of detail about how the code _was_
run, the repository builds trust that:
1. the people who wrote this code knew what they were doing,
2. they did that thing well, and
3. what they did made sense (which you can judge for yourself).

## Documenting dataset structure

The code itself is lovely. Take their [preprocessing file][Preprocessing]. Each 
part of the data-table has a comment, e.g. "I7c" is "If someone insults a man, 
he should defend his reputation with force". Maybe we can't know the _answers_. But by at least knowing the structure, we can follow along the analysis.

Maybe it's good that the writer knows the reader won't have access to the data. 
That way, no understanding is assumed. Often the problems with science code (or 
just code in general) is that subject-matter-experts assume everyone has a 
certain level of background and thus skip explanation.

But [the average person knows less than you think][xkcd]. I'm giving my thesis
proposal / qualifying exam talk on Thursday, and I know there are people from
the non-science parts of my life coming. You also have those people (probably).
Try aiming to explain to them, if reasonable.

----

I haven't looked into the backend of social science studies before. If they're
all as good as this one about documenting their code, maybe we hard-science
folks could learn a thing or two.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/sghai9/technology-mediation-csea
[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1038/s41586-026-10525-4
[Preprocessing]: https://github.com/sghai9/technology-mediation-csea/blob/main/qmd/1a_preprocess.qmd
[xkcd]: https://xkcd.com/2501/