---
layout: post
title: How verbose is that log?
subtitle: Debugging woes
tags: [debugging, logs]
author: Faith Okamoto
---

I've had a run of very frustrating debugging recently. This post is inspired by
one of the issues I ran into: a verbose log that left out crucial information.

## Project background

Our tool performs *read alignment*. It takes a genetic sequence and looks for 
the best *alignment* for it. As an intermediate step, we create *chains*. The
best few chains are turned into full alignments.

Each chain gets a plausibility score. Each alignment gets a quality score. While
we hope that the top-scoring chains correspond to the top-scoring alignments, 
that's not a given. My project is to help us find higher-quality chains. That 
often, but not always, leads to higher-quality alignments.

## What I wanted to know

When I run comparisons of my code vs. the old version, some of the alignments
are worse. (Some of them are also better, y'know.) For a few of these, I turn on
verbose logging and check their chains. Often my code found a higher-scoring
chain which just so happened to turn into a worse-scoring alignment. Not much I
can do there.

The interesting ones are where I found a lower-scoring chain. Recently I simply 
could not figure out why my code was failing to find the higher-scoring chain.
As far as I could tell, my code could see the better chain's path. But for some 
reason I wasn't using it.

## The culprit

Eventually I found the issue. (Of course I found the issue; otherwise I wouldn't
be writing about it.) In between chain creating and chain logging, the chains
were rescored. During chain creation, I found an even higher scoring chain. But
its score dropped more during rescoring. Thus it was logged as a lower score.

This was frustrating. I'd been chasing ghosts the whole time. This was just
another instance of a higher-scoring chain making a worse-scoring alignment, but
now with the higher score being *hidden*, instead of logged as normal.

## Takeaways

Now that I've subjected you to a page worth of case study, what have we learned? 
Mainly that a verbose log _shouldn't leave important steps out_. What counts as 
"important"? Obviously you don't need to log _everything_. But, use this test:

**If a step could not be inferred from the verbose log, the log has failed.**

These logs are, ideally, usable by people other than the folks who originally
developed the code. I wasn't in the room when rescoring was added. There was no
way for me to spontaneously know that it was to blame.

Here, a very important number was calculated and then *recalculated* before
actually being logged. If you're doing something as important as that score
recalculation, it should be logged. Some other examples of things which _are_
in the verbose log, and definitely need to be there:

* When picking between multiple alignments, we report the score of each. In this
way the reader can know how good the alternate alignments were.
* When attempting to create chains, we report the number of the "zip code tree" 
(think "cluster") that is currently being processed. This helps with debugging
zip code trees.
* The fact that we have two "chaining" steps (one makes "fragments" which the
other strings into finished chains) is very explicit.
* The name of the sequence currently being aligned is prominently presented.
* The way that some distances are decreased due to "backing up" is explained.

Make your verbose logs actually verbose, folks. That's what they're there for.