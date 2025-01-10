---
layout: post
title: Useful error messages
subtitle: How did I mess up?
tags: [errors]
author: Faith Okamoto
---

Since I made two recent [pull][rpvgPR] [requests][vgPR] about graceful errors, I 
figured I'd talk about why this is so important. In general, you should try to
anticipate common issues the end-user might run into. Those errors should cause
useful, descriptive error/warning messages.

## What's a useful error message?

Well, here's some non-useful error messages, sorted by progressive usefulness:
* Nothing
* "Program error: segmentation fault"
* "Matrix is invalid" (especially if the user doesn't obviously input a matrix)
* "Cannot parse [file]" (without further details)

By contrast, here are some useful error messages:
* "`--years` argument must be positive"
* "Attempted to read [file] that does not exist"
* "Matrix is not diagonalizable, an assumption of the Foo algorithm"
* "[file] has an invalid CIGAR string on line 72"

See the pattern? A useful error message tells you what went wrong and provides a
clear path to fixing it. File not there? Probably a path typo. Input doesn't
follow specification? Look up the specification, figure out a fix. And so on.

## Why bother?

No one will ever use your program exactly as intended. They'll *try*, sure, but
unless they're being spoon-fed what to type, there's a natural cycle of try,
fail, fix. The goal of an error message is to get the end-user to "fix".

This is especially important for common errors that would have weird, seemingly
unrelated error messages. For example, that [`rpvg` pull request][rpvgPR] arose
from me being confused about a segfault. I tried to figure out what could've
gone wrong in the code to no avail. Finally I realized that I'd messed up a
file path. Fixing the file path fixed the segfault. A typo'd file path causing a 
segfault was extremely non-obvious.

So, I added a better error message. One quick check for file existence, and now
I could tell the user exactly what went wrong: the file path being wrong. They
can now jump straight to "fix" by double-checking file locations.

If you tell your end-user what went wrong, they can diagnose the issue quicker.
An experienced programmer/researcher probably has the ability to self-diagnose
an issue, but why make them? If there's a common failure case, give it a common
and useful error message.

[rpvgPR]: https://github.com/jonassibbesen/rpvg/pull/69
[vgPR]: https://github.com/vgteam/vg/pull/4489