---
layout: post
title: Keeping a "dry lab" lab notebook
subtitle: What did I do yesterday?
tags: [process]
author: Faith Okamoto
---

I define "dry lab" as "science with computers" (e.g. data analysis), "wet lab"
as "science with physical things" (e.g. mice), and "field work" as "science
outdoors" (e.g. specimen collection). My wet lab courses taught how to keep a
[lab notebook][LabNotebook]. I mostly hear of them for wet lab or field work.
Since I keep a lab notebook for my dry lab work, I thought that I'd explain.

## What goes in a lab notebook?

Everything.

Okay, that wasn't very helpful. Obviously I don't mean *literally* everything
(e.g. you don't have to write down when you took your lunch break). Still, it
really doesn't hurt to take too many notes.

I tend to keep a different notebook for each project. At the top goes the
project name and my contact information. Note the contact info: the purpose of
is to be shared, both with my future self but also with lab-mates.

Each day is given a section heading. As I keep my notebooks in Google Docs, this
conveniently lets me jump to any day I like by clicking on the heading in the
sidebar. Under that section heading is more or less a stream of consciousness,
including:

- Summaries of what I just did
- Description of what I'm trying to do. (I should write this *before* doing the
thing, but sometimes it gets written while the thing is running)
- Description of any problems (lack of files, runtime error, bugs, etc.)
- Brainstorming/current thoughts
- Notes on results, especially intermediate ones
- Images, especially of plots
- Copy-pastes of code, especially anything run interactively
- Summaries of meetings
- Links to online resources I'm referencing (documentation, GitHub issues, Stack
Overflow answers, blog posts, etc.)

This is not a [README][README]. For one, a README is much better structured.
It's edited, rearranged, organized. It's meant for a reader to be able to do 
something. My lab notebook is meant for a reader to know what I did.

## Example notebook entry

This is part of a notebook entry dated 13 Nov. 2024. You can see me working
out what I want to do in real time in that first rambly paragraph. Then I
summarize what I'm about to do, and paste the exact line of code I used. Finally
I think of something else relevant. The entry continues after this bit with what
I did to address my own concerns.

> Worked a little more on slides & the project summary this morning. Wasn’t able
to meet with Ed to discuss the rotation, because he is currently sick. I added
an automatic ignorance of homozygous samples. Now the filter thresholds need
further thought. If you have 100 samples, you may be okay with 5 having opposite
bias (for example), but if 50 of those are homozygous (optimistically), then you
may only let 2 of the remaining samples have opposite bias. I think I will
implement two levels of filters: a percentage and a maximum number of homozygous samples. The percentage will be of all heterozygous samples, rounded down. Say
0.05 opposite and 0.1 neutral - then 0.85 of heterozygous samples would be
biased the same way.
> 
> I’m going to try this with a file that has all 4,053,098 biallelic SNPs in the
5 samples. I’ll allow the 1 defect to be either neutral OR homozygous. Most of
the SNPs will never have a scan done.
> 
> `python3 code/find_biased_segments.py PAV/all.vcf.gz omnic omnic/biased_segments.csv --max-neutral 0.2 --max-homozygous 1`
> 
> Oh, I also have to worry about missing genotypes. I’ll combine them with
homozygous.

## Why record all of that?

Because I forget what I just did. I trick myself into thinking I must've done,
or at least intended to do, what I now know to be right, and then I am confused
about why it isn't working. Or I dive into scripting, start hacking my way
around issues, and lose sight of the original purpose of the script. Or I forget
the list of steps I'm supposed to follow for the project. Or someone asks what
parameters I used for that thing I did last week.

Then I look back at the notebook entry and remember.

My lab notebook is how I make sure my science is reproducible. Yeah, I don't
have clear-cut experiments like a wet lab tech who runs gels all day. But the
tiny parameter tweaks or bug-fixes that are my day-to-day are just as important
as chemical concentrations, if I want it to be possible to repeat and understand
what I just did. Science doesn't count until someone else can use it.

Keeping the notebook digitally is a big part of why I find it so easy. I can
copy-paste code and images with ease, and then search the document for keywords.
I can also show it to someone else easily: just send them a link.

----

If more of my lab-mates kept such notebooks, and I could read them, then maybe
I'd understand more of what they're doing. Maybe I'd find more connections to
my own work. Maybe I'd just find it cool.

I wouldn't know. No one has ever shared a dry lab notebook with me.

[LabNotebook]: https://www.science.org/content/article/how-keep-lab-notebook
[README]: https://www.makeareadme.com/