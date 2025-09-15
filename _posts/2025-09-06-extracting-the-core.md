---
layout: post
title: Extracting the core
subtitle: More ways to DRY that code
tags: [refactoring, dry]
author: Faith Okamoto
---

One of my projects finally inched close enough to "good" that I sent it to for 
code review. (I should blog about code review at some point...) I got the PR 
back with comments, then spent some time refactoring. I want to talk about a
non-obvious refactor that I'm kicking myself for missing earlier.

----

I'm going to try to explain this in a way that leaves out all the details of 
science and implementation. This blog is targeted at scientists *in general*,
after all, which means in aggregate I can only assume as much knowledge as an
[average layperson][XKCD].

## What used to exist

We have a "zip code tree" data structure which stores "seeds". The point of a 
zip code tree is to quickly find distances between its seeds. Due to things that 
I do not want to explain, this requires a lot of delicate, non-obvious, nested 
logic. That's not a problem by itself.

The problem is that I query the zip code tree in *three separate places.*

If you know of the [Don't Repeat Yourself (DRY) principle][DRYBlog], this is a 
massive violation. Similar fiddly logic repeated across multiple files? Eww.

## Why hadn't I fixed it before?

I know about DRY, obviously. I had to rewrite that fiddly logic in those three
separate places. I carefully commented to explain each location. So why didn't I 
realize the a chance to DRY this code?

Basically, because the shared fiddly logic was interspersed with bespoke code in 
each location. There was no distinct section to stick into its own function. One 
place only needed to use part of the results, another needed to cross-check each 
seed against a lookup table, etc. The core logic was tangled up with other code.

## The solution

As I mentioned, this was kicked off by a code review. The reviewer noted how
fiddly the logic was in multiple places. He also seemed to get confused by the 
intertwining of the stuff required for core logic and the stuff required only 
for that particular use of the zip code tree.

I read his comments and realized I could kill multiple birds with one stone, by refactoring that core logic into its own function. So that's what I did. Now I
have a function whose *sole purpose* is to handle all the fiddly logic used to
query the zip code tree. That's it. Nothing else. No filtering, no cross-checks,
no reshaping the results into a format more convenient for the outside
algorithm. My function just queries the zip code tree, then dumps all the seed
results out in the most obvious possible format.

Doing so *massively* improved readability. Now each query location no longer 
had to handle its own fiddly stuff. Disentangling the core logic from the 
outside requirements means that they can't be confused for each other. If both 
the core logic and this specific location mess with the orientation of a seed, 
then they can mess with it separately. Obviously, cleanly, separately.

----

Making code DRY isn't just a matter of moving, say, a block of forty lines into
its own function. You also have to look at the code and consider: is there some
logic which shares *conceptual* parts with other places? Can I extract that core
logic to simplify each place it appears?

Who knows, the answer may be yes!

[DRYBlog]: https://faithokamoto.github.io/2025-03-14-dont-repeat-yourself/
[XKCD]: https://xkcd.com/2501/