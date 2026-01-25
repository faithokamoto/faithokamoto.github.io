---
layout: post
title: Sometimes the example should be big(ger)
subtitle: Or at least not teeny
tags: [documentation, tutorials, examples]
author: Faith Okamoto
---

I've mentioned that I'm [cleaning up vg's wiki pages][RevampingBlog], yeah? 
Well, it's is coming along. Slowly. Mostly when I'm procrastinating. Case in 
point: ["Evaluating alignment performance using simulation"][EvalutatingWiki] 
got a rework in the last two hours of a Friday because... because, okay!

That rework was a win-win situation: the page isn't hilariously out-of-date
(seriously, the thing had last been touched in 2017), and I get a blog topic.

## Runnable examples

One of the big issues was a severely lacking example. I mean, there _was_ code. 
But its files weren't available. You were to follow along with your own data.

Sure, folks referencing this page probably do want to run this workflow on 
their own data. But there might be inconsistencies between files, intricacies 
of processing, simple file corruption, or other reasons for someone else's 
files to be unusable. Having a working example makes it easier to figure out 
what exactly is wrong. (And who to blame.) Just find the difference! Plus, this 
way a user can test out the workflow even before they have their own data.

I knew I was going to want to leverage some of the files that already existed 
in the [`test` directory][TestDir]. Those are shipped with the repo.

## Choosing an example

I've talked a bit about [creating toy data][ToyDataWiki] before, but here I'll
discuss how I thought through the test case for this particular wiki page.

The general workflow that I wanted to demonstrate was:

1. Acquire graph reference & comparable linear reference
2. Generate reads with simulated known-truth positions
3. Align reads using vg & another tool
4. Compare read alignments

This limited the examples graphs considerably. I had to use a big enough file.
Why did the file have to be big? Because I needed some of those reads to align
_incorrectly_. If the example was so small that both aligners work perfectly,
then the comparison wouldn't do anything interesting. A complicated enough graph
would have messiness so some reads would align to the wrong position.

I flipped through `test` and got a BRCA2 graph. Just the ticket. A clinically 
significant locus of non-negligible size and non-negligible variation.

Anyhow, now my example was great. It was:

- Runnable
- Using a biologically interesting region
- Large enough that a few reads failed

Voila! New wiki example!

[EvalutatingWiki]: https://github.com/vgteam/vg/wiki/Evaluating-alignment-performance-using-simulation
[RevampingBlog]: https://faithokamoto.github.io/2025-10-25-revamping-documentation/
[TestDir]: https://github.com/vgteam/vg/tree/master/test
[ToyDataWiki]: https://faithokamoto.github.io/2025-03-02-the-art-of-toy-data/