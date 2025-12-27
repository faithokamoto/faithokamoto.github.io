---
layout: post
title: Quality of life updates
subtitle: one of those easy things to neglect
tags: [errors, usability]
author: Faith Okamoto
---

I've been on holiday, so this will be a quick one. We have a release scheduled
for Monday that I suspect I'm going to end up doing. That led to me looking at
the changelog for this update. There is a... pattern.

## The pattern

Most changes fall into the category of "new/better feature". Tweaks to an
algorithm, updating index files to a new format, making a tool more flexible.
And I'm not saying that I _don't_ do that: in fact, I have a rather notable
bugfix going out this release.

But I'm the majority source of the other kind of change: the "quality of life"
update. Making a command print helptext, adding warnings if an output file will
be (likely unexpectedly) empty, changing a verbose crash to a single-line error.

## Both are important

The first group, with substantial improvements, are necessary. If our tool
didn't do anything then no one would use it. Developing new algorithms and
whatnot is the bread and butter of a methods bioinformatician; this is literally
our job. So I understand why most people focus on doing that to perhaps the
exclusion of other activities.

Yet, quality of life improvements are also necessary. If our tool was impossible
to use (instead of merely hard... sorry folks) then no one would use it. Things
can become popular because they're supremely effective. But they can also
become popular because they're easy to figure out.

This is why I try to push a quality of life update whenever I run into a spot
that could use a fix. Even if it's not blocking me. Given my experience, I can
figure out my way around problems. But having to leverage that experience isn't
ideal. So I end up doing a bunch of minor tweaks in the course of my work.

----

Do I wish more folks set aside time for quality of life updates? Yeah. Then I
could use their stuff, heh. I've written this post in the hopes that simply
defining the categories could be useful to some reader.