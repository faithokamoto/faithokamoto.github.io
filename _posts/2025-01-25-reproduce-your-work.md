---
layout: post
title: Reproduce your work
subtitle: (Ideally somewhere else)
tags: [process, last-pass]
author: Faith Okamoto
---

Here's another post about something that's relevant to my last week. (I will
get around to another [code critique][CritiqueTag] before the month ends, I
promise, to my nonexistent readers.)

I just wrapped up a [rotation][Rotations] project. This involved polishing my
[README][README], writing a summary of my results and next directions, giving a
presentation, all that jazz. It also involved me reproducing my results.

## Why reproduce your own results?

I mean, they're your results. Presumably you trust them and you know how they
were found. (If you don't trust your own results, then you haven't finished the
project.)

But therein lies the rub. You know how those results were found, which means you
alone know all the back alleys, weird hacks, and detours that you took along the
way. Can you be sure that you remember all of them at once, though? If you
handed this project off to someone else, would you be able to tell them exactly
what to do, sans all the detours?

**To be sure a complete, polished workflow truly functions, you must run it.**

This final workflow compilation is infinitely valuable. What tools did you use?
What obscure flags? What shortcuts? Why are you confident in your own results? 
Presumably you ran some tests on them which came back well. Put those tests into
your final workflow, so others can run it and understand. You and those others
both will know, once and for all, what you did and how you did it.

Plus you'll find errors somewhere. I just guarantee it. It doesn't matter how
well you took notes, how carefully you kept your clean code up-to-date. If you
run it for a 'last' check, it will error somewhere.

## How to reproduce your own results

This section comes with a caveat that, sometimes, you can't actually run some
parts of your full workflow. Maybe there was that one simulation that took a
week once you finally got it working. But you took [notes][Notebook] on how you
ran it, right? In these cases, just copy the exact code into the finished
workflow. You can still test all the stuff around it.

All the many steps I took in my project eventually got compressed to a single
script (which, granted, called other scripts/tools) that takes around a day to
run. How do I know it takes a day? I ran it with `time bash code/workflow.sh`.
Yep, that simple.

Start from your input data. Document its locations. How was it preprocessed? Put
that in the workflow. What was done next? What intermediate files were made?
What tests did you run? All goes in the workflow.

A workflow doesn't necessarily have to be a script. It could be an English
description of a set of actions to do. It could even be incorporated into the
README, as a list of scripts to run. Just make sure that a person with no
knowledge other than the workflow would be able to run the script. "Use the
lab's ref genome directory" isn't useful. "Use `/groups/okamotolab/ref_genomes`
on the `genome` server" is. The key is document, document, document everything.
Have the very last step of the project be re-running the workflow, even if you
tested it before. Voila. Reproduced.

## Things I ran into when reproducing my own results

Just for fun, here's a non-exhaustive list of issues I had to fix in the
workflow script I made for my project:
* I've been using an input FASTQ file for so long that I forgot where it was
from. Upon digging through my notes I found its origin directory and that it
used to be a BAM file. I had to add the code to transform the BAM into a FASTQ.
* When reformatting the order in which I gave arguments for a command-line
script, I accidentally gave the same positional argument twice. I was very
confused why the code was complaining about unknown arguments - I saw the 
argument, right there!
* Several paths were accidentally relative to the directory `workflow.sh` was
run from, including e.g. tools that I'd downloaded elsewhere.
* I had to document the conda environment used.
* Several options I'd used "in the moment" to fix an issue were missed. I had to
re-diagnose the issue and re-add the option.

Hopefully these examples give you an idea of the kinds of errors you only 
catch when running a workflow over again. Try reproducing your own work! It's...
I won't call it *fun*... quite illuminating.


[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[Notebook]: https://faithokamoto.github.io/2024-11-23-dry-lab-notebook/
[README]: https://www.makeareadme.com/
[Rotations]: https://www.rootedinstem.com/grad-school/v0wsho73avs7hsa9bg1dxdxvdriz59