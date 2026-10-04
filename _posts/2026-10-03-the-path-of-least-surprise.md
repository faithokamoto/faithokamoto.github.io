---
layout: post
title: The path of least surprise
subtitle: another minor usability update
tags: [usability]
author: Faith Okamoto
---

I come to you with yet another tale of woe, i.e. a small annoying problem that a
fellow student was suffering with in silence but which wasn't actually all that
hard to fix. Let's take a look.

## The goal

Among the many things my lab's software [`vg`][vg] does is make these dotplot
visualization things.

![dotplot](https://user-images.githubusercontent.com/145425/32562417-83cf82a8-c4a6-11e7-80e0-4addc61612ca.png)

There are nodes, edges between them, and then paths drawn to follow edges. Each
path gets a color & emoji assigned via hash of the path name. The problem was
that the color/emoji combos would change from picture to picture. Instead of
having, say, the path corresponding to sample HG002 being shown consistently.

## Why was that happening?

Because the code was made in a way that didn't consider this overall user
experience. Remember how the path name was being hashed to get a color/emoji
combo? We were including path range subsets in the hash. That is, if you took
a snapshot of the graph, and then took another snapshot shifted downstream by
100bp, because those are in different locations, we'd hash them to be different.

This is very reasonable from the programmer end. Those subsets are different
from the main path, and we store the location in the name. Then when we want to
has the name, the easiest thing is to pass the entire path name to the hash
function. If you only consider a single resulting image it'll always be
reasonable.

But, again, it's still _surprising_ that the color/emoji changes when you shift
the path. The end user has no real conception of the path subsets being
completely different. From their end, they just want to match up paths to the
high-level things that they think about, and those high-level things are the
main paths. Thus it doesn't make sense to have different subsets end up looking
different.

## Removing surprise

Ideally, software does what a user expects it to do. It may be sometimes
_reasonable_ for it to do something different. Still, if it's _surprising_, then
that requires the user to figure out why the thing looks weird. Avoiding user
confusion in the first place is Important and Useful. People want things to Just
Work. So it would be nice for this to Just Work.

Anyhow, I [changed it][PR] so that the hash now uses the base path name instead
of the subset path. That is, I removed the location from the hash. This means
that any subset of the same main path will result in the same color/emoji,
significantly easing matching things up across pictures.

Voila. The path of least surprise.

[PR]: https://github.com/vgteam/vg/pull/5041
[vg]: https://github.com/vgteam/vg