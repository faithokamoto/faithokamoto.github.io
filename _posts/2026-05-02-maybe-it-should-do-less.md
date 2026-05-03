---
layout: post
title: Maybe it should do less
subtitle: an ode to simplicity
tags: [pipeline, usability]
author: Faith Okamoto
---

Yeah, I work on the behemoth that is [vg], but this post is about the benefits
of task-specific tools. Instead of a be-all end-all multi-functional soup. 

---

## The impetus

I work mostly on `vg giraffe`, a tool that does "read alignment". It has *a lot*
of parameters. Thus, we have a [separate workflow][lrg] for running parameter 
searches. Ideally, the pipeline does read alignments with a bunch of different
parameter combinations to find the optimal values.

Only, you may note that the repository is called `long-read-giraffe-experiments`
and not, say `giraffe-parameter-search`. That's because we sort of grafted on 
parameter searches to a honker of a Snakemake. Originally, this workflow was 
built to test `vg giraffe` against other tools on a variety of input data. You 
can see why someone might have put these together at some point in time.

1. Running various tools on the same data to compare performance.
2. Running various parameters on the same data to compare performance.

But, as we shall see, mixing the two led to problems.

## The problem

Did I mention that the Snakemake is a honker? The current version is 6,322 lines
long. Since purpose #1 requires harmonizing the inputs and outputs of a bunch of 
tools, quite a bit of space is taken up by non-`giraffe` drivel. The overlap 
that #1 and #2 has is also problematic when folks start updating the #1 pathway
(important, especially for the [paper][preprint]) and cause random breaks in #2.

From the perspective of a gal just trying to do a parameter search (i.e. me,
last week) this means that the current workflow is bloated with irrelevant code
which has a tendency to break the parts I care about. And then it's hard for me
to debug and fix stuff since I don't want to mess with the moving parts of #1.

## The solution

As foreshadowed in the title, the solution is to get a divorce.

We're extracting the parameter search code into its own entity. Presumably it 
will become shorter and cleaner once it's given top and sole billing. This new 
thing will also get dedicated documentation. It will never have to worry about a 
secondary purpose. It will have one purpose. Only one. Run parameter searches.

---

Hopefully this little case study demonstrated why it can be problematic to
combine mostly unrelated things into a single tool. Soup is easy because you
just throw everything in. But therein lies the problem: it's hard to separate
out again. Even the bad bits. They'll stay mixed in.

Try to avoid soup, when possible.

[lrg]: https://github.com/vgteam/long-read-giraffe-experiments
[preprint]: https://doi.org/10.1101/2025.09.29.678807
[vg]: https://github.com/vgteam/vg