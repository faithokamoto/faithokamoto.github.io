---
layout: post
title: How I document code
subtitle: A brief overview of my process
tags: [process, last-pass]
author: Faith Okamoto
---

If you scan through this post, you might notice that there's no code. Yep, I'm
writing a blog post about how to document code without including any code.
Instead, I'll step through the higher-level plan I use for code documentation.

## Define goals

I define what I'm doing before I start coding. What requirements do I have? What
constraints? What logic am I trying to implement? What final products do I need?
For example, I draw flowcharts or hand-sketch figure layouts. Creating a basic
README at this stage also helps.

By knowing what I'm doing, I'm less likely to spend time on code going nowhere.
(I still do. Just less.) I have a framework to justify choices. I have a
concrete goal to improve towards. I have pre-made words to explain my code.

## Write readable code

I know, easier said than done. Still, I actively try to keep my code
understandable. This applies even, perhaps especially, during its development.

Mainly, I write code that will need less refactoring. I avoid "temporary" names:
if I'm creating a variable, function, file, etc., I give it a useful name (e.g.
`parent_id`, `time_delta`), instead of e.g. `dt2` or `func`. I use whitespace in
between chunks of logically separated code. I put commonly reused code into
functions, and commonly reused functions into helper files. I add terse comments
about tricky logic. This way, cleaning up the code later is easier.

## Add [docstrings](https://peps.python.org/pep-0008/#documentation-strings)

(Or the equivalent for whatever language I'm using.) The first step after
finishing the first-draft of my code is to make sure I have usable docstrings.
This means both creating docstrings or carefully checking my pre-existing ones.

The process of writing docstrings calls attention to useless parameters, useless
functions, more readable/logical ways to write or call the function, etc. Also,
as my code tends to use functions/methods as major structural elements, this
provides an overview of the code's layout.

## Overexplain

Yes, I have a stage with even more comments than what I release to others. Here
I do fine-grained refactoring. I step through the code, adding way too many
comments, increasing readability (without compromising functionality) in every
way I can think of. All those ways, however, are out of the scope of this post.

Now, my code is probably bloated, but at least other people can read it fine.

## Final check

Time to de-bloat the beast. I scan through the code again, removing redundant
comments, clumping code that used to be apart, and generally removing my
readability improvements. "But I just added all of those!" you may complain.
Well, now I take them out. But only some of them.

The idea of this step is to reap the rewards from refactoring. I don't *need*
that many comments, since the underlying code is readable enough as-is. That's
why I specify removing *redundant* comments. This step increases readability, as
the remaining essential comments will be even more prominent.

## Conclusion

Your ideal process will probably look different than mine. However, I urge you
to consider if your current process could be changed to prioritize better code.
Do you currently write the first stream-of-consciousness implementation that
comes to mind? Do you currently put comments and other readability improvements
in the "do eventually" category? Do you currently omit docstrings?

Remember, you're writing code for the world *and* your future self.