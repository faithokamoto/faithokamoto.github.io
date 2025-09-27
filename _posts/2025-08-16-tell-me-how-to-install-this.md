---
layout: post
title: Tell me how to install this
subtitle: August 2025
tags: [published-code-critique, readme, installation]
author: Faith Okamoto
---

I admit this [\[published-code-critique\]][CritiqueTag] is slightly petty. The 
paper promised a new method quite relevant to my research interests. Yet the
details are nowhere in the preprint. I ended up having to dig through section 7
of their [supplementary note][Supplement]. At that point, I figured I might as 
well check their source code too. I didn't even get that far before finding 
things to critique.

This month's paper: Salehi Nowbandegani P. Defining and cataloging variants in 
pangenome graphs. *biorXiv* 2025. doi: [10.1101/2025.08.04.668502][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Wait, this table of contents is lying

The first thing that most people will read is the [README][README]. That's its 
point. If I'm lost in a sea of new code, I want a map with an arrow. PSA: the 
arrow should actually point somewhere.

The [README][PantreeREADME] here has a table of contents with an "Installation"
link. Great! Except that link goes nowhere. There is no installation section.
The other three sections ("Introduction", "Usage", and "Command Line Interface")
all exist. But there's no instructions on how to install. So the table of 
contents is lying.

### Explaining how to install is really important

The second thing that people will do, after orienting themselves via the README, 
is try to install the tool. That is, if they're going to use it. And presumably
if you released the thing, you want people to use it.

That's why missing the "Installation" section is a particularly big loss. This
tool seems to have both a command-line interface and a Python interface. (Or at
least that's what I assume, given the two usage examples.) How am I supposed to
set that up? That probably requires something beyond a simple `git clone` of the
repo, right?

- What do I need to do in order to `import` functions/objects into my own custom
scripts? Does that require particular file locations, running a pre-processing
step, etc.?
- What do I need to do in order to use the command line interface? Do I need to
add something to my `PATH`, for example?

The installation section, or somewhere near it, would also be a great place to
explicitly call out the [dependencies][Requirements] required to run this.

### This might be intentional, but still

After further consideration and digging, the lack of installation instructions
may be intentional, and related to the lack of the `pantree` executable/script
(don't know which) itself. Maybe the authors are hiding that until they get the
paper accepted? That's still a little icky. The preprint is out, so they have
timestamped proof of primacy.

And even if this *is* intentional, don't have the section be missing! It'd be 
better state that installation is impossible at this time. That way no one tries 
and fails to use the code.

----

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/oclb/pantree
[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1101/2025.08.04.668502
[PantreeREADME]: https://github.com/oclb/pantree/blob/main/README.md
[README]: https://www.makeareadme.com/
[Requirements]: https://github.com/oclb/pantree/blob/main/requirements.txt
[Supplement]: https://www.biorxiv.org/content/biorxiv/early/2025/08/04/2025.08.04.668502/DC1/embed/media-1.pdf