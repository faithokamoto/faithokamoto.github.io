---
layout: post
title: Documenting options
subtitle: What choices do I have?
tags: [documentation, parameters]
author: Faith Okamoto
---

I recently identified a problem with `vg filter`'s `--tsv-out` option. Namely,
that a command to write "a tsv of the given fields" didn't document which fields
were possible. This command is quite important to running QC on our GAM and GAMP 
alignment files. Those files aren't human-readable, so if a user wants to, say,
get mapping quality by read, there isn't a better way.

Without clearly documenting the possible options, how can a user know that not
all GAM fields are available? For that matter, some of the fields aren't even in
the GAM; they're calculated on the fly.

A key part of writing code usable by others is telling them what it can be used
for. Don't hide useful options. So I went through `src/readfilter.hpp` and wrote
down each possible field. A [wiki][Wiki] makes it discoverable and linkable.

The lesson to take from this is to **always document the available options**
for a multiple-choice argument. Before I have to come along and do it for you.

[Code]: https://github.com/vgteam/vg/blob/master/src/readfilter.hpp
[Wiki]: https://github.com/vgteam/vg/wiki/Getting-alignment-statistics-with-%E2%80%90%E2%80%90tsv%E2%80%90out