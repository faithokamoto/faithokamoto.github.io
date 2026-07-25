---
layout: post
title: Magic scripts still need documentation
subtitle: and organization
tags: [published-code-critique, readme]
author: Faith Okamoto
---

As always I forgot to grab a paper to critique until the end of the month. At 
least my lab's journal club is soon so I can just grab the paper we'll be
discussing then.

This month's paper: Wouters D *et al*. SubCellSpace: Automated characterization 
of subcellular mRNA localization patterns in spatial transcriptomics. *arXiv* 
2026. doi: [10.64898/2026.04.28.720613v1][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### What is "standard"?

There are several modules present in the repository. I chose to look at the
[`raw_spatial_data_processing`][Module] one since that seems to be what a
researcher would want to try on their own data. Theoretically there are some
scripts which handle everything for you.

Opening it up I'm greeted by a README. Yay! Except it's not quite detailed 
enough to understand. For example, here's how to organize input files:

> The scripts assume your data follows the standard folder structure of raw Spatial Transcriptomic data, but can be adapted.

... okay, but what is "standard"? Standards change over time, differ between
labs and tools, and aren't obvious to someone trying to dip their toes into a
new field. If I want to try out the pipeline, how do I organize my test files?

This could be easily fixed by either describing in the README itself what the
file structure should look like (my preferred way) or at least by linking to an
explanation hosted elsewhere, e.g. in the documentation for somewhere that
creates the expected input files.

As is, though, the README's description is unhelpfully vague and doesn't provide
any pointers about how to un-confuse myself.

## Maybe have your flags be command-line options?

The README also lists a few flags which the user may wish to modify. But
wouldn't these be better as command-line options? That way they are properly 
shown someone _running_ the magic pipeline script. Plus you can set command-line
options such that the user has to input a value, forcing people to make a choice
about what to input.

In any case, it's also not clear where to find these flags and how to set them.
It turns out that they're in the `.py` scripts, but after the massive list of
imports, so somewhat hidden. Also, since they're global variables, it's a bit of 
set-and-forget. Again: command-line options let you force users to input values.

## Don't put everything on the top level!

And reading carefully the `.py` files in question, they have one of my pet
peeves: a bunch of code in the top-level/global area, instead of inside of a
function or just `if __name__ == '__main__':`.

Leaving all this code lying around means that _it may be run unexpectedly_.
It's a [boilerplate guardrail][SOLink]. You may think you don't need guardrails,
but I guarantee you that if you leave off the railing someone else will get
distracted or confused, and run off the edge.

In addition, it's poor organization. Some things in the global namespace are now 
actual global variables (like those flags I was talking about) and some are part 
of the pipeline. What runs when I run this script? Ideally, I would be able to 
check out a central entry point, but instead the entry point is... everywhere.

Which compounds the issue of a lack of documentation. I really don't know how
this thing works, what its analysis flow should be, and in order to figure that
out I have to read all this outside stuff instead of a simple main-space.

----

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/sifrimlab/SubCellSpace
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.64898/2026.04.28.720613v1
[Module]: https://github.com/sifrimlab/SubCellSpace/blob/main/raw_spatial_data_processing
[SOLink]: https://stackoverflow.com/questions/419163/what-does-if-name-main-do