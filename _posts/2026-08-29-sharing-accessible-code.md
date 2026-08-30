---
layout: post
title: Sharing accessible code
subtitle: for the greater good
tags: [publications, code-availability]
author: Faith Okamoto
---

I'm first non-first author<sup>1</sup> on a paper that should be submitted 
Tuesday.<sup>2</sup> This meant I spent a good portion of Thursday reading 
through the nearly finalized text. I'll discuss one of my comments here.

### Code availability policies

Plenty of journals have a code availability policy. The first one I submitted a
paper to, *G3 Genes|Genomes|Genetics*, has it under "Availability of data and
materials"<sup>3</sup>:

> G3 requires all authors to publicly release all data and software code underlying any published paper as a condition of publication.

Straightforward, right? A section titled "Data Availability", drop a link to
GitHub or Zenodo or wherever else you put your scripts, and you're off to the
races. Right?

Not so fast.

### Non-available availability

There are a lot of ways to release nigh-unusable code. I won't name names, but 
here are some that I've found:

1. Code that won't run. Possibly it never ran on any setup other than the
original developer's computer. In any case, the code is there, but useless.
2. Code that has bad [documentation][DocumentationTag]. For examples of bad (and 
good!) documentation, check out my monthly [code critiques][CritiqueTag]. The
code is there, and maybe it's theoretically possible to run, but no one can
understand it well enough to do so.
3. Code that requires contacting the authors to obtain. I think this is falling
out of favor, but I've read quite a few older papers with "scripts are available
via email", and that means you have to ask someone and then they have to
cooperate. Needless barrier.
4. Code with unclear references. Let me explain that one more.

### Clearly referencing code

This is what I was commenting about on that paper. (It's been fixed, and it was
a mixup rather than intentional, so I'm not blaming anyone.) There were many
places where the Methods section would say things like:

> The foo statistic was calculated with a custom R script (foo_calc.R)

Why is this a problem? They told me what the code was, right? Well, I know what
name the researcher used for that code file<sup>4</sup>. I have no idea what was 
_in_ the file. If you want to reference scripts by name, sure, do that, but you 
still need to tell me where they are. Link the GitHub repository at the start of 
the section. Or link each script. Or any other way of allowing me to navigate 
from "I'd like to see how they did that" to the place in question.

----

Truly available code should be easy to find and easy to use. Yeah, yeah, I know,
that's hard. Research is hard. Writing papers is hard. Make it easier for the
rest of us to figure out what you did, m'kay?

---

1. By this I mean I'm fourth author, since there are three first authors.
2. Or it really should be, but the first of these "we're submitting the paper by
DATE" deadlines I heard was around a year ago. This time we've actually managed
to get a finished text and sent it to all the peripheral coauthors, though,
which bodes well. Also there's a larger package we want to get into.
3. I apparently did this too well; the editor had me do extra work to format
stuff even better than policy required, because they wanted to use my code as an
example for others. Or something like that. I'm paraphrasing my memory here.
4. Though sometimes they left the `foo_calc.R` bit out.

[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[DocumentationTag]: https://faithokamoto.github.io/tags/#documentation
[G3Avail]: https://academic.oup.com/g3journal/pages/author-guidelines#section-5-9