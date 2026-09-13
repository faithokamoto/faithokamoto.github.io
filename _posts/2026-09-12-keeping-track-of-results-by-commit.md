---
layout: post
title: Keeping track of results by commit
subtitle: easy and useful
tags: [process, notebook]
author: Faith Okamoto
---

I develop, implement, and test algorithms as part of my research.<sup>1</sup> On
a day-to-day basis, that looks like a lot of fiddling. Fiddle, test, fiddle,
test. How do I keep track of what's what in my [notebook][NotebookBlog]?
Mostly, I notate results alongside their commit hash.

## How do I keep track of commits?

The script I use the most for my tests is set up such that whenever it runs, it
prints out the current commit that my local repository is on. This is easy via
`git rev-parse HEAD`. I will then write down the first few characters in my
notes. For example, I may use a table comparing "old" (typially the master
branch) vs. "new" (typically my new algorithm branch). Each of these will also
have a three-character commit hash alongside.<sup>2</sup>

I didn't use to do this; I used to just write "old" and "new". Why'd I change?

## Why keep track of commits?

A wet lab notebook may record the exact amounts of reagents used or at least the
protocol followed. The algorithm is my protocol. It changes with each commit, so
by remembering which commit was used, I can later replicate my experiment.

And both "old" and "new" will change over time. The master branch is continually
updated<sup>3</sup>, occasionally in ways that will affect the output I check.
Obviously my "new" branch changes with each fiddle.

If, obviously completely hypothetically, I accidentally torpoedo my results and
everything goes to pieces, I can easily back up to whatever the last working
commit was. And I'll know exactly which one had reasonable results. No guessing
required for which change was the problem.

----

A shorter one today since I also wrote on Monday. I do like discussing my
process, and this is what y'all get. See you next time.

----

1. My primary research, really. Aims 2-4 of my thesis proposal.
2. I find that three characters is typically enough to disambiguate things. Also
it fits easily in my table.
3. Recently, I've been making bugfixes for things I found in the process of
testing my new branch. Finding a problem and being able to say "it's not me it's
them" is *great*. Because usually, it is me :D

[NotebookBlog]: https://faithokamoto.github.io/2024-11-23-dry-lab-notebook/