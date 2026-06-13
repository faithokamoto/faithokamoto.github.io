---
layout: post
title: Removing deprecated subcommands
subtitle: for fun and profit?
tags: [deprecated, tech-debt]
author: Faith Okamoto
---

I was _supposed_ to be starting a new project this week, now that the qualifying
exam is behind me, but the time I had allocated to thinking got spent, um,
handling old vg issues. At least this was useful? I think it was useful.

In particular, I took a look at our bunch of deprecated subcommands. Some very
*old* deprecated subcommands. And thought that maybe I could just toss 'em.

## Why deprecate things?

Deprecated subcommands print out the following message:

> Subcommand [name] is deprecated and is no longer being actively maintained. Future releases may eliminate it entirely.

That's basically it. We use deprecation as a way of marking features that we
aren't planning to put any further work into. Things might break. Default 
behavior could downgrade. Just... we no longer care.

Why deprecate instead of removing wholesale? Well, we'd had these subcommands
for a while. Used them in our own workflows. In case someone's relying on this
functionality, it's polite to it them around. Not updated, sure, but frozen at a 
version that was OK at some point in time. The warning lets folk gradually move 
away until we eventually get around to removing the cruft.

## Removing deprecated things

About "removing the cruft". Well, [`vg sift`][PR4930] and [`vg join`][PR4932] 
were deprecated by a [PR made in 2020][PR3136]. It has been about five and a 
half years since the end of 2020. The warning has been around for a while.

It was time.

These subcommands [have bugs][Issue2199] and [don't work as expected][Issue2515]
and also just... haven't been maintained in over half a decade? We really don't
want folks to use them. Nor are they even useful; `vg sift` can be replicated by 
the well-maintained `vg filter` if you're willing to put a little legwork into 
parsing a TSV, and `vg join` does a thing we don't generally want any more.

So I deleted stuff. Lots of stuff. The subcommand files, for one, but then also
the implementation functions that only they used. Combined that's over 1,500
lines of code that I tossed out the window. 

## Who does this help?

Codebases tend to grow. That makes it harder to find what you need, harder to 
onboard someone, harder to keep all the pieces working together. Being able to 
meaningfully delete useless code is a sadly rare occasion. 

Removing this stuff makes it just a bit easier for the next newbie who wants to
contribute. It makes it just a bit easier for the folks who might try to use a
broken feature and confuse themselves. It makes it just a bit easier for the
maintainers who don't have to keep those files from breaking the build.

Also, it made me happy.

----

Hopefully this was a useful, or at least interesting, walkthrough of a decision
I made today. (Literally toady; check the timestamps on those PRs.) I'm
travelling tomorrow but I just had to write about this tech debt cleanup
because it was so fun. And I think there's a paucity of easily accessible
thought-process explanations from tool maintainers. This blog is my small
contribution to that canon.

[Issue2199]: https://github.com/vgteam/vg/issues/2199
[Issue2515]: https://github.com/vgteam/vg/issues/2515#issuecomment-544903318
[PR3136]: https://github.com/vgteam/vg/pull/3136
[PR4930]: https://github.com/vgteam/vg/pull/4930
[PR4932]: https://github.com/vgteam/vg/pull/4932