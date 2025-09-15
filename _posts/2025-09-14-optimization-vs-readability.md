---
layout: post
title: Optimization vs. readability
subtitle: What is a "microptimization"?
tags: [refactoring, optimization]
author: Faith Okamoto
---

This is somewhat of a mea culpa after my [previous post][ExtractBlog] on
refactoring. But then, not entirely. I did end up having to revert the pretty
refactor, though.

## What's more important than readability?

That's a question people ask looking for a cop-out. The answer often is "time". 
Grant deadlines, graduation, teaching responsibilities, vacation etc. and whoops 
well I guess we just have to go with whatever messy code we have on hand. Just
take a look at some of my [critiques of published code][CritiqueTag].

But there's also code *speed*. Sometimes, the most optimized version of your
code will be significantly slower than the more readable version. Even if given 
infinite time (hah), I understand picking the former. Sometimes.

## Micro-optimization

Not all speed optimizations are made equal. Some reading, from Stack Exchange:
"[Is micro-optimisation important when coding?][MicroOptQ]"

If this is a bespoke data analysis script and the question is whether it runs
for five hours instead of four and a half, even that 10% speedup probably isn't 
worth it. On the other hand, if it's an algorithm meant to be built upon and 
used by lots of people, a 1% slow down might be too much.

There's also the wrinkle that many people (me included) aren't great at
intuiting which parts of their code are causing slowdowns. That's why it's
helpful to have a [profiler][ProfileQ] and run tests of each version. Only with
that sort of hard evidence can you really be sure which parts of the code are 
worth optimizing, and which parts can be safely left alone.

## Why'd I revert that readability refactor?

Recall that the [refactoring I made][ExtractBlog] was to take some logic used
across multiple locations, and stick it in its own function:

> My function just queries the zip code tree, then dumps all the seed results out in the most obvious possible format.

That was the problem. There's overhead involved in saving results in an
intermediate format, passing them out, and then going through them again. That
overhead was something that I ended up not being able to justify to myself.

Such disappointment doesn't mean I've given up this logic as a loss for
readability, however. I never surrender code to the abyss of incomprehensibility
without a fight. I'm going to try to simplify this logic in some other way. 
Probably I'll have to have similar logic in three places again, but that logic 
will be much less complicated. I'll find a way to make this readable without
the crushing overhead costs of a separate function/iterator.

Well, I'll figure that out later. It's still the weekend, after all :D

[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[ExtractBlog]: https://faithokamoto.github.io/2025-09-06-extracting-the-core/
[MicroOptQ]: https://softwareengineering.stackexchange.com/questions/99445/is-micro-optimisation-important-when-coding
[ProfileQ]: https://stackoverflow.com/questions/375913/how-do-i-profile-c-code-running-on-linux
[ReproduceBlog]: https://faithokamoto.github.io/2025-01-25-reproduce-your-work/