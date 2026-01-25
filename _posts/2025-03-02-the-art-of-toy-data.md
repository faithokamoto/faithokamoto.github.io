---
layout: post
title: The art of toy data
subtitle: How and why to make small test data
tags: [testing, documentation, examples]
author: Faith Okamoto
---

A recent [class project][bach] had me creating and documenting a small Python
script (`bach`). As part of this process, I made toy data. This post will go
over the process I used.

## What is toy data?

Toy data is a very small example dataset. It probably isn't "real", and it's
probably so small as to have no value to science. Its value lies in enabling a
short and simple test of the program. The benefits are manyfold:
* Check if the program was installed correctly
* Demonstrate standard syntax by example
* Quick test case for sanity-checking changes to the code

Ideally, the toy dataset is small enough that the program's algorithm can be
worked through by hand. If an end-user has difficulty understanding what a
program does, they can use the toy dataset to figure out the kinks.

## How to make toy data

What does the program do? What is the *simplest* case to demonstrate? Multiple
datasets are fine. Better to have many examples than an overly complicated one.

Toy data should, if at all possible, be human-readable. Only use binary or
compressed files if there absolutely necessary. ([My toy data][bachTest] uses
[BAM binary files][SAMspec] because the human-readable counterpart SAM can't be
sorted/indexed as `bach` required.) It should be *very very tiny*. So tiny that
uploading it to e.g. GitHub, and having everyone who downloads the tool also
download the data, is no problem at all.

Handmade toy data is usually the best option. You can carefully choose data such
that exactly what you want will occur, and nothing else. For `bach`, I handmade
the [VCF][VCFspec] using an example VCF as a base, but I didn't want to manually
generate BAM files with enough reads to make sense, so those were made by a
simple helper script.

Toy data goes in a clearly labeled directory (e.g. `test`). It should be made
before the actual program, and it should be a test case during development.

## How to use toy data

First, it's a [test case during development][TestDrivenDevelopment], right? 
Great. Then, once you're more or less done with a minimum viable product,
document it! Create a model command which uses the toy data. (I actually made 
[two][bachExamples], demonstrating different modes of `bach`.) Document the
command. Make sure it works. Publish it.

Congratulations, you've just made toy data.

[bach]: https://github.com/faithokamoto/bach
[bachExamples]: https://github.com/faithokamoto/bach?tab=readme-ov-file#examplestests
[bachTest]: https://github.com/faithokamoto/bach/tree/main/test
[SAMspec]: http://samtools.github.io/hts-specs/SAMv1.pdf
[TestDrivenDevelopment]: https://en.wikipedia.org/wiki/Test-driven_development
[VCFspec]: http://samtools.github.io/hts-specs/VCFv4.2.pdf