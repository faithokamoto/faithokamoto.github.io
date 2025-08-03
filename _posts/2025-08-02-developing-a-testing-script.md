---
layout: post
title: Developing a testing script
subtitle: Yes, tests are still development
tags: [testing]
author: Faith Okamoto
---

As [promised][AutomatedTestsBlog], I'll dive into a case study on a testing 
[script][OptionTestScript] I developed recently. Hopefully after reading this
blog post, you'll have a better understanding of how to craft useful tests.

## Identify the need

First, before writing a test, you should be able to say what the point is.
Writing tests is not easy. It *is* easier than dealing with the aftershocks of
buggy code. Still, you're putting in up-front effort for the hope of having an
easier time later. Similar to a vaccination.

I knew exactly what problems I wanted to prevent. In [`vg`][VG], a command-line 
option must be declared within an array, added to a string, *and* handled by a 
`switch` statement. Plus, the helptext should be consistent with how the option 
actually worked. I'd spot-fixed several bugs arising from this inconsistency.
Thus, my goal was to automatically catch such errors before they caused issues.

In addition, I figured I'd address my other helptext pet peeve: auto-wrapping.
If the description of an option was too long, the terminal auto-wrapped it to
the next line. All well and good. Except that the auto-wrap put description 
*underneath the list of options* instead of in the side column. I wanted all the 
descriptions to stay in their column.

## Come up with specific goals

1. For all command-line options, check if the helptext, array, extra string, and 
`switch` block all match.
2. Ban over-long helptext lines. I decided on an 80 character maximum, similar
to [PEP 8][PEP8], but a round number.

A unit test checks the code against some ideal. That means it's important to
have a specific ideal to compare against. I had some basic ideas:
* Check all the `src/subcommand/*_main.cpp` files
* The helptext should have, for each option, an optional shortform followed by a 
longform, then an optional argument hint, and finally a description
* Descriptions and options should all line up in neat columns
* Lines mustn't be more than 80 characters
* The presence/absence of an argument hint should match what's in the array
* ...

Once I had a vague idea of what I was doing, I jumped in to writing code. All I
had to do was check that each specific rule was followed, right? How hard could
that be?

## Allow *explicit* exceptions

Of course it wasn't that easy. I had been thinking of how to fix normal cases.
But there were several instances that my script offered up as errors, which I
decided to allow after consideration.
* Two files, `help_main.cpp` and `test_main.cpp`, had a completely different
structure for command-line options, and thus I couldn't parse them. I allowed
my script to skip those.
* I'd initially planned to ban duplicate options from appearing in the helptext.
However, I found that `annotate_main.cpp` had a legitimate reason to display the
same option twice (once per "mode") and thus I let those go.
* While the `--help` option was more-or-less standardized across all files, in
`giraffe_main.cpp` it activates a special long version of the helptext. Thus I
allowed that file to have a nonstandard description for its `--help` option.

The key here is to make the exceptions explicit, and to explain why each was
allowed. What you're testing will always end up being more complicated than it
first appears to be. These explanations make it easy for someone later to pick
up and understand the test.

## Be flexible to catch wrongness

I had in mind several simple ways for the options to be inconsistent with each
other, or for the helptext to be misleading. What I didn't properly anticipate
was the sheer number of ways for things to go wrong.

A lot of this manifested in parsing the helptext. I developed regexes to extract
the option names and catch the argument hint. However, these regexes were
initially far, far too strict. They would ignore lines which were improperly
formatted. Combined with how I allowed options to be excluded from the helptext
(which occurs for deprecated or developer-only options), this meant the helptext 
could be wrong but the script would ignore it.

I had to constantly check for "false negatives" where my script failed to raise
errors. My regexes are now more flexible. If something is wrongly formatted,
I'll still parse it. But I'll then attach a bad-formatting error message to be 
printed later.

Having my code at least parse wrongness was important to make it visible.

## Check that everything is actually being parsed

I ran into issues with files that had their helptext function, switch statement,
etc. formatted in a way that I didn't expect. The overall structure of my script
involved four separate full-file scans, each looking for a specific part of the
file. They'd read until they found the start of their block, then return once
the block finished.

Unfortunately in some cases they'd terminate early, thus failing to parse the
rest of their assigned block. This is the invisibility problem again. When I 
eventually realized the root of my issue, I added more checks to make sure that 
option lists were compatible with each other.

Remember, in order to find an issue, the test has to find *something* first.

## Add more requirements as they come up

I tacked on a bunch more rules that I hadn't initially thought of. Some late
additions include:
* Require both `-h` and `-?` to be aliases of `--help`
* Require the default case of the `switch` statement (i.e. what gets called for
an unknown option) to fail/error/etc.
* Require the helptext to indent options by exactly two spaces
* Allow deprecated options to take an argument and not use it (due to erroring
instead)
* ...

As I developed my script (which involved running it, fixing the problems it
flagged, adding more test case rules, etc.) I learned more about what a normal
subcommand file should look like. Or, I guess, I developed stronger opinions.
Those opinions then got encoded into my testing script.

## Detailed error messages are good

But in the end, I'm not really the target audience of this unit test. The "end
user" is just some person who makes a PR to `vg`. If this script fails their
code, it's helpful to fail verbosely and specifically. Therefore I made an
effort to include [actionable error messages][UsefulErrorsBLog] for each failure
case. The script isn't meant to be punitive. It's just meant to prevent the
introduction of bugs. Thus, it should probably explain what bug it thinks is
being introduced.

----

No one had bothered to write this kind of test case before. Honestly, it's
probably because [`vg`][VG] is science code. It's pretty good for science code 
(I mean, it has automated tests), but in general people focus on developing
their own little parts. Looking at the package as a whole, and considering the
user experience, aren't required parts of the paper-writing process.

Unless I'm here, because I care about this sort of stuff :D

[AutomatedTestsBlog]: https://faithokamoto.github.io/2025-07-14-automated-tests/
[OptionTestScript]: https://github.com/vgteam/vg/blob/master/scripts/check_options.py
[PEP8]: https://peps.python.org/pep-0008/
[UsefulErrorsBlog]: https://faithokamoto.github.io/2025-01-10-useful-error-messages/
[VG]: https://github.com/vgteam/vg