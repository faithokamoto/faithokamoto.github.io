---
layout: post
title: Updating explanations of meaning
subtitle: When what your code does changes
tags: [last-pass, science-meaning]
author: Faith Okamoto
---

This topic I really could not figure out a better way to summarize in a few
words, so y'all have to deal with a confusing title. 

## What am I talking about?

The basic idea is that code has meaning. Perhaps a data structure represents an
alignment of DNA sequences as a two-dimensional list of characters, or an
algorithm calculates distances by looping through defined lists of endpoints.

You may have some wonderfully [documented][DocumentationTag] code. But now it
needs a change. Reshuffling the order of items, rejigging the algorithm so that 
a step has a different goal, reworking [assumptions][ExplainBlog]. Now those 
explanations are outdated.

## But that seems obvious

Yes, it seems obvious that when you change what code does/means, you should also
change how that code is explained. But many people don't.

In the weeds of code changes, debugging, all that fun stuff, comments might 
simply be ignored. Then, once everything works, it's left alone. I get it. Once 
all the *code* is done, you just want to be finished. The same reason people 
fail to document the first time around. After all, *you* remember what changed.

This is how we end up with confusing documentation referencing outdated versions
of the code. Which is even worse than no documentation. If a clueless person
(e.g. you in a month) tries to follow it, they'll be confidently wrong.

## What to do instead

You probably don't want to constantly update comments as the codebase evolves. 
That's why this post is tagged [\[last-pass\]][LastPassTag]. Once the change is somewhat settled, it's time to do one more read over the relevant code. Simply
double-check the documentation and bring it up to date.

It's annoying. But it pays off. I promise.

[DocumentationTag]: https://faithokamoto.github.io/tags/#documentation
[ExplainBlog]: https://faithokamoto.github.io/2024-12-07-explain-your-science/
[LastPassTag]: https://faithokamoto.github.io/tags/#last-pass