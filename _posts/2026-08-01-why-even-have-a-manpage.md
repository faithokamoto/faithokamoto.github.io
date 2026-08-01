---
layout: post
title: Why even have a manpage?
subtitle: at least keep this up to date!
tags: [manpage, documentation]
author: Faith Okamoto
---

Among my many<sup>1</sup> side projects is one to [update our manpage][ManPR].
I'll write about that. Not the update itself *per se* but why I care.

## What's a manpage?

Well, if you ask [Wikipedia][ManWiki], it's

> a form of software documentation found on Unix and Unix-like operating systems

Which means, yes, this is me going on about documentation again.

To give an example, you can the [Linux `cat` command's manpage][CatMan] has:

- A **name** ("cat - concatenate files and print on the standard output")
- A **synopsis** demonstrating how to call it
- A brief **description** of what it does
- A list of all command-line **options**
- A few **example** invocations
- **Metadata**: authors, how to report bugs, copyright, etc.

This places the command in context: not only what options exist, but also why
you might use it. Also, the manpage is available online, making it easy to 
reference or link.

## What's _our_ manpage?

The [`vg` manpage][VGMan] is *mostly* a list of our `--help` outputs. At the top
it also includes lists of subcommands grouped by category. And that bit is
*very* important. There are a lot of `vg` subcommands<sup>2</sup>. Though we
have `vg help` to list all subcommand names, the manpage goes into more detail
about what options are available. And honestly, often you need the option list
to really understand what a subcommand does.

It is useful to have a collection of subcommands in one linkable page. That's
all our mange is really trying to be: at the top, a brief overview of what our
tool can do, and after that, the helptext for all of the relevant subcommands.

## Why am I fixing this?

Because it's ridiculously out of date, like a lot of the rest of our
documentation was<sup>3</sup>. There are many subcommands which no one ever
bothered adding to the manpage list. For example, I use `vg gamcompare` to
compare GAM format alignment files. One is the truth, and I want to know how
close the other is. This is [in a tutorial][CompareTutorial]<sup>4</sup>. But
`vg gamcompare` is nowhere in the manpage. It might as well not exist.

If the point of a manpage is to have a single place summarizing what our tool
can do, then we need to actually, y'know, include all that our tool can do.

----

For anyone else with software that you expect other people to use: it really,
really is helpful to have an online manpage overview.

----

1. Probably too many. Depends on who you ask. I find them relaxing, and often
making connections across time and domains of our tool is useful to my work.
Though I might be able to get the same benefit with, say, half the time.
2. Less than there used to be. I removed four deprecated ones between `v1.75.0`
and [`v1.76.0`][v76].
3. Also better than it used to be, because of my improve-the-wiki side project.
4. Granted, I added it to the tutorial.

[CatMan]: https://linux.die.net/man/1/cat
[CompareTutorial]: https://github.com/vgteam/vg/wiki/Evaluating-alignment-performance-using-simulation
[ManPR]: https://github.com/vgteam/vg/pull/4979
[ManWiki]: https://en.wikipedia.org/w/index.php?title=Man_page&oldid=1365386649
[v76]: https://github.com/vgteam/vg/releases/tag/v1.76.0
[VGMan]: https://github.com/vgteam/vg/wiki/vg-manpage