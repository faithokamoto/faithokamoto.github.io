---
layout: post
title: Not every speedup is snazzy
subtitle: An optimization is an optimization
tags: [optimization, algorithms]
author: Faith Okamoto
---

I've been doing optimizations because my code that used to be winning on speed
is now losing on speed. Or, actually, it was half-winning last I checked, but
that was after several rounds of optimizations. Thought I'd write on it.

----

## What I thought doing algorithms would look like

When I got into this I was really enamored with algorithms. Such beautiful ways
to look at biological problems, reduce them to diagrammed lines of code, and
elegantly glide towards a solution. I basically assumed that I would get to be 
staring at whiteboards a lot dreaming up high-level algorithms. And then
debugging them. I enjoy debugging, so long as I'm not stuck for overlong.

I mean, I get to do that, but then I come to times like today.

## What the profiler told me

So, my code was slow. OK. Let's see why. I ran under `callgrind` and pulled up
the logs. I could see what functions were taking up time. Then smush them.

Before when I did this, I looked at the offending functions and then thought of
ways to, for example, modify my overall algorithm for efficiency. Save an index
so I can jump to it instead of iterating through all the middle stuff, for
example. But today I was seeing slow functions that I had no "control" over.
Helper stuff that I called as necessary.

## Doing less than necessary?

But maybe I didn't need to call all of those helpers. For example, there are
several functions which essentially page through an index looking for a bit of
info. Those bits of info exist in a line of the index. Paging through a book to
get to page 4, then restarting and paging through to get to page 3, etc. is
rather inefficient.

So I wrote a function that pages through the index once and gets all the
necessary info in that one go. Worked like a charm. A nice minor speedup.

Elsewhere, I saw that we were spending a lot of time on a lookup for a value
that was actually calculated elsewhere and stored for easy access. So I reused
that lookup. A nice minor speedup.

Elsewhere, I was spending a while with `.at()` lookups on a vector. It was
possible to swap it for an iterator, so I did that. A nice minor speedup.

And a bunch of minor speedups combined is a noticeable speedup.

---

Trust me when I say that none of these were beautiful changes. What they were,
was practical. Being smarter about doing less work even when the high-level
algorithm is the same.