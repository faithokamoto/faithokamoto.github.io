---
layout: post
title: Commit your clunkers
subtitle: Yes, even those ones
tags: [version-control, screed]
author: Faith Okamoto
---

I just got back from a conference talk which reminded me that I had a screed.
So, a screed<sup>1</sup>. I want you to **commit your clunkers**<sup>2</sup>.

----

## What do I mean by "clunkers"?

I mean your terrible no good very bad code. Messy drafts, painful hacks, 
undocumented slush piles, data magic held together by duct tape and prayers. If
you've written real-life code, you know what I'm talking about.

Maybe written on a tight deadline: a lab meeting presentation tomorrow and two
data tables needed to be smushed together. Maybe a random one-off and you
figured it would never be used again. Maybe just copy-pasted from an LLM and
you're not even sure if it works properly.

Those things. The clunkers. Put them under version control. Do it now.

## But why?

Because later you will thank me, that's why.

Okay, you wanted a more detailed explanation? Well, let's take those possible
reasons one by one.

- **Script made on a deadline for a lab meeting?** You're going to want to
extend it later. Someone will have a suggestion for a little further analysis,
and a prior version to work off is a blessing. Don't reinvent the wheel. Start
with a thing that works. That is _known_ to work.
- **Random one-off functionality?** Yeah... you know these things are _never_
just one-offs, right? Three months down the line, someone's going to ask you to
do it again, since you did it before, and you're going to want to have that
exact working version saved somewhere.
- **Questionable copy-paste?** It's still _a version_. Put it under version
control. This is part of properly attributing where your code came from. It also
makes it easier for you to see which parts you change, as you tweak the code to
better fit your purposes. Fiddle a line here, a line there, swap this to that,
and instead of relying on your memory to keep everything straight, you'll have
nice little diff marks telling you what changed from the prior version.

If the script is doing something useful, or at least trying to do something
useful, then commit it. The bones can always be repurposed later.

## You're not my mom

You're right, I'm not. (If I am, uh, contact me? Something went terribly wrong.)
But I have an opinion and a blog. I believe I've defended my opinion here. You
are, of course, free to disagree.

----

Anyhow. Commit your clunkers, people!

1. Should I make a tag for this? I think I will. And will add it to some older
posts.
2. Yes, that is a word. [Clunker][ClunkerDef]:
    > someone or something notably unsuccessful

[ClunkerDef]: https://www.merriam-webster.com/dictionary/clunker