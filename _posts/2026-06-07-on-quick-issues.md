---
layout: post
title: On quick issues
subtitle: totally not just laziness
tags: [development-process, github, mentorship]
author: Faith Okamoto
---

First off, I passed my qualifying exam, yay! Then I took a trip. So this will be
a shorter post than normal, just me musing about something that happened this
week. That thing being some polishing of my undergrad's project, a pipeline to
[perform parameter searches of `vg giraffe`][parampipe].

---

## What happened

Elina (that's her name) has been working on this for a while. Specifically,
according to chat logs, since 27 April. On 14 May she pushed an early version to
GitHub, and on 1 June I tried to use it.

I immediately ran into a whole host of problems. Minor things, mostly: a memory
limit needed to be raised, one of the random sampling methods was returning
unexpected results, etc. Things that I could fix myself by spending some time
to look at the code. Some of them I _did_ fix myself because I needed a fix
right away in order to continue using the pipeline.

But I didn't just commit over Elina's commits. Instead, for the two things that
I saw a solution for immediately, I opened pull requests. Then for the others I
opened quick issues. And moved on with my day.

## What I mean by "quick issue"

Take [issue number 3][issue3] as an example. I saw a weird thing in my log file,
copied the warning into GitHub, and put why I thought it was an error.

That's a quick issue. A "help thing broke" note.

Importantly, this doesn't mean a _lazy_ issue. A lazy issue would have been me
just copying the bit of the logfile (or worse, the entire logfile) without
including any surrounding context. It's important for even these quick issues to
be verbose enough to make it clear what went wrong and why it's a problem.

A quick issue is a minimum helpful report. Enough information to understand it
and for whoever fixes it to be sure that the fix is for the right thing. Just no
effort for a solution. No effort to understand how the issue came into being.
It's an effect, not a cause.

## Why did I just open quick issues?

I could've fixed these things, probably. I know the underlying programming
languages, I have access to some of Elina's notes, and I have more experience
than her in science coding. That latter being due to nothing fancier than the
simple march of time.

But, for one, she's my mentee. I want to train her to be able to be part of team
coding wherever she ends up, and that means getting practice with pull requests 
and issues. She should be able to handle the whole process from issue intake to 
fix. The only way I've ever properly learned how to computer is by *doing*; 
lectures or artificial tutorials don't cut it.

Also I'm lazy. I think the proper term of art is "busy" :) But indeed, I had 
other things to do. In particular I was prepping for my thesis proposal 
presentation on 4 June. It wasn't my job to fix that code, so I didn't.

---

Hopefully you can see why I opened quick issues, and how quick issues can still
be helpful all round as long as they're not lazy issues. So that's my quick
defense of quick issues. Till next time!


[issue3]: https://github.com/vgteam/giraffe-parameter-search
[parampipe]: github.com/vgteam/giraffe-parameter-search