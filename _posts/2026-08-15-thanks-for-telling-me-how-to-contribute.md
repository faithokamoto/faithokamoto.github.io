---
layout: post
title: Thanks for telling me how to contribute
subtitle: (that's not sarcastic I mean it)
tags: [published-code-critique, documentation, guidelines]
author: Faith Okamoto
---

I recently added a [`CONTRIBUTING.md` file][vgContrib] to the tool I work on. 
Thought I'd check out what other tools have. After about thirty seconds of 
trying to think of a well-used bioinformatics tool which isn't Minimap2 (I've 
[done that before][Minimap2Blog]) I came up with BioPython.

This month's paper: Cock, PJA *et al.* Biopython: freely available Python tools 
for computational molecular biology and bioinformatics. *Bioinformatics* 2009. 
doi: [10.1093/bioinformatics/btp163][DOI]

## Original code

This tool is on [GitHub][Code]. I'm focusing specifically on their 
[`CONTRIBUTING.rst`][Contrib].

## Critique

Remember that "critique" has a neutral meaning which can also involve praise :)

### Opening with what you don't know you need to know

The point of files about how to contribute is that you read them before, well,
trying to contribute. That is, the audience is *explicitly* newcomers. Ever
tried to write for newbies? It's harder than you'd think. There are a million
and one ways to not understand something, and if you already have a robust
understanding, you often take things as standard knowledge.<sup>1</sup>

This is why it's very useful for the file to open with stuff that a newbie might
not be considering. Stuff like licensing, how to use Git version control, etc.

### Explaining tests

A good software project will have tests, full stop.<sup>2</sup> The exact form,
location, and usage of those tests, however, won't be obvious to the new person
just stumbling in. That's why it's important that this file specifies how to run
unit tests and links to further documentation about them.

> Any new feature or functionality will not be accepted without tests. Likewise for any bug fix, we encourage including an additional test. See the testing chapter in the Biopython Tutorial for more information on our test framework: http://biopython.org/DIST/docs/tutorial/Tutorial.html

> Please always run the full test suite locally before submitting a pull request, e.g.:
>
> ```
> $ pip install -e . --group dev
> $ cd Tests
> $ python run_tests.py
> $ git commit ...
> ```
>
>Have a look at the related chapter in the documentation for more details.

### Explaining contributing at all

As a meta-comment: just _having_ a `CONTRIBUTING` file is useful. This info is
the stuff that experienced folks know already, but having it all written down
means that new folks won't have to struggle through painful initial steps. Or, I
mean, there will probably still be struggle, but not _as_ painful as it would've
been.

Long-term usable software, the kind that gets cited for years, has to be
maintained. Unless you want all the burden of that maintenance to fall on a
single point, you need <strike>fresh meat</strike> new contributors, and keeping
those around tends to require help. This file is help.<sup>3</sup>

----

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

----

1. [Obligatory XKCD][XKCD]
2. My mother worked as a quality assurance engineer for a good portion of my
childhood. This is me channeling her spirit.
3. Were we missing one for over a decade? Yes. But now we're not, and that's
what matters.

[Code]: https://github.com/biopython/biopython
[Contrib]: https://github.com/biopython/biopython/blob/master/CONTRIBUTING.rst
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1093/bioinformatics/btp163
[Minimap2Blog]: https://faithokamoto.github.io/2025-12-13-understanding-an-api/
[vgContrib]: https://github.com/vgteam/vg/blob/master/CONTRIBUTING.md
[XKCD]: https://xkcd.com/2501/