---
layout: post
title: Documenting the magic button
subtitle: When simplifications become confusing
tags: [documentation, pipeline]
author: Faith Okamoto
---

I've been running someone else's pipeline (that most terrible of tasks) and, 
unsurprisingly, have issues. This post will be about one of those issues.

## All-in-one-pipelines

There's a particular fantasy that scientists (and people in general) like to
engage in, where you can just press a button and a complicated task is done.
Maybe you need a simple [config file][ConfigBlog]. But otherwise, everything
Just Works. No need for writing bespoke code, or understanding how the magic
button works under the hood. Nope! We want everything to Just Work.

This fantasy persists because it would be so useful if we really did have magic
buttons for every conceivable task. Problem is, we don't.

Maybe the button works for a very particular use case (probably whatever its
designer was trying to do), but step outside of the box and all of a sudden
things break. Depending on how well the pipeline is set up, it may be flexible
to a little breakage. But at this point the most likely scenario is you have to
get your hands a little dirty with the inner workings.

## What I was doing

I wanted to run a pipeline that would compare variant calling results from two
alignment algorithms. Conceptually this is simple: run both algorithms, input
their results into the same variant-calling tool, and compare for accuracy.

The twist is that, for various reasons, it would be a lot simpler for me to use
my own reference files, instead of the ones in the standard directory. No big
deal, I thought. I'll just change the input directory to my own.

What I hadn't considered was that the oh-so-helpful magic pipeline follows some
very specific rules as to how the files have to be named. If you're running any
of a wide variety of pipelines, and you're pointing to the standard directory,
then the magic button will find the correct files and happily hum along. But my
files had a slightly different naming scheme. Thus, the magic pipeline couldn't
find them. I had to figure out the naming scheme and then make my files match.

## What would've helped

I accept that the magic is useful in this case. By specifying only a directory
and a base name, the pipeline is set up to find all the necessary files. But,
for me as someone who needs to tweak the parameters, it would've been useful to
_know how the magic worked_. This could mean a brief description of the file
naming scheme used, for example.

Yes, sure, wrap the pipeline in a magic button. But for the sake of those who
need to step outside of the box, sufficient documentation about the results of
minor tweaks (such as changing file locations) is immensely useful. Documenting
these assumptions makes the pipeline more flexible.

[ConfigBlog]: https://faithokamoto.github.io/2025-10-04-config-files-vs-hardcoding/