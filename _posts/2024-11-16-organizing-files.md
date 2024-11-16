---
layout: post
title: Organizing files for code
subtitle: Folders, scripts, and data oh my!
tags: [process, file-level]
author: Faith Okamoto
---

Today I'll discuss a meta-issue: not what you put *in* the code, but where you
put the code. I'm not so arrogant as to think my way of organizing is the best. 
Instead, I'll discuss what I do, and explain why. Take what you'd like.

## My file organization

Upon starting a project, I make a new directory. It's named something relevant,
e.g. `y_mt_assoc` for an association study of the Y and MT chromosomes. The 
first file is a [README][README]. It explains the directory's purpose.

Within the main directory, I create `code/`, `data/`, `log/`, and `results/`.
Each does what it says on the tin: logfiles are in `log/`, data in `data/`, etc. 
Typically there will be sub-directories, especially in `data/` and `results/`,
but those are project-specific and also often not immediately obvious.

Each script is named for what it does. For example, `find_biased_regions.py` is
a script which finds "biased regions". Its [script docstring][ScriptDocstrings]
would explain the scan and define what a biased region was. However, such
details are too wordy for the filename.

Sometimes code files are "helpers": only used from other files. For example, if
many of scripts use the same custom input/output functions, I'll make a helper
which consolidates those. This abides by the [DRY principle][DRY]. Helper files
have the suffix `_helpers`, e.g. `io_helpers.py`.

## Why do I use this organization method?

I love consistency. It's why I can get around my apartment in pitch black: I
know where everything is. If I need to quickly grab a logfile, I know exactly 
where to look. Same for searching through all the code from a project because I 
vaguely remember that one file had some useful function.

Besides finding files I need, this also makes *writing code* easier. I don't
have to spend any thought on where I should write results to. They all go in
`results/`. I/O is one of the most finicky parts of any program, and this
reduces overhead. While I still document assumptions (e.g. "GRM filenames are
relative to `data/GRM/`"), it's easier when the assumptions are standard across
scripts. I might later add robustness by e.g. accepting files as command-line 
arguments, but in early development I just want a thing that works *now*.

A consistent naming format makes it easier to find the script I need, and makes
it easier to know what everything does at a glance.

Plus, the README. I cannot stress enough, please [make a README][README].

[DRY]: https://www.geeksforgeeks.org/dont-repeat-yourselfdry-in-software-development/
[README]: https://www.makeareadme.com/
[ScriptDocstrings]: https://faithokamoto.github.io/2024-09-24-script-docstrings/