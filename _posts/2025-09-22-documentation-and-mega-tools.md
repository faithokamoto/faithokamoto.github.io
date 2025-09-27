---
layout: post
title: Documentation and mega-tools
subtitle: September 2025
tags: [documentation, readme, getting-started, published-code-critique]
author: Faith Okamoto
---

As is probably obvious from [my blogging history][SearchResults], I work on the
[`vg` toolkit][vgGitHub]. And if there's one thing vg is known for (besides our
papers with cool results and all that), it's that, while the toolkit is quite
powerful, it is a pain to get into. Sheer complexity has overwhelmed many a
casual user trying a "simple" analysis, and many a developer tinkering with a
"small" change.<sup>1</sup>

The solution would be [documentation][DocumentationTag]. I mean, while we *do*
have a [README][vgREADME] and a [wiki][vgWiki], both have room for improvement. 
So, this month I'll do an unusual [code critique][CritiqueTag] in that this
isn't code for a single paper. We'll look at the documentation available from
the perspective of a brand-new user.<sup>2</sup>

## Original code

The source code for the `vg` toolkit is on [GitHub][vgGitHub].

## Critique

To be extra-super-clear, since I am talking about my workplace here, nothing
that I'm about to critique is anyone's *fault*. Nor does it necessarily reflect
badly on anyone.

**Documentation is hard**. Especially for such a big tool. Especially with 
deadlines (conference etc.). "Whoops, ran out of time to make a wiki page." And 
surely someone will get to it later. Right?<sup>3</sup>

### But I want to do [insert specific thing]

The README and wiki pages do a *decent* job of providing commands for many
common use cases. But we don't have an article for everything. For one example,
it took until [May 2025][FilterWiki] for there to be a page on how to get
per-read statistics. That's a very common quality-control/comparison operation.
By the point it had a wiki page, it was [over a year old][FilterPR].

This poses an issue for our hypothetical newcomer. Perhaps they've come to vg
because they heard that it's a powerful, multi-use toolkit. But if there isn't
good documentation on a workflow matching their specific use case, then they'll
have to string together commands from all over the place. Knowing how to find
the important bits is incredibly difficult for unfamiliar tools.

### Out of date documentation

The wiki sidebar links a ["vg manpage"][vgManpage]. You'd think this would be
incredibly useful. Ideally it would show a complete list of commands and what
you can do with them. But [it's not automatically updated][ManpageIssue]. Thus,
someone trying to use it as a reference for an up-to-date version of vg might
just end up confused.

Also, we have things that are just plain [broken links][WholeGenomeWiki] due to
pages moving around over the years.

Obviously the problem of documentation aging poorly isn't unique to large
projects. However, the risk is higher because of the size: changes by one person
may make documentation from a different person now incorrect, despite all
involved working in good faith to the best of their knowledge. Plus, there's
simply more documentation in the first place, which means more to upkeep.

### Finding the useful bits

Okay, let's assume that our newcomer wants to do something that actually has an
existing, up-to-date wiki page. How are they going to find it? The wiki
[homepage][vgWiki] is more or less just a list of article titles with some
headers. It's not even a *complete* list of article titles.

Then, we have the issue of not all the content being obvious from article
titles. For example, the article ["Changing References"][ChangingRefWiki] has
information on how to fiddle with a "GBWT" to change how individual paths are 
stored/interpreted as references or not. Someone reading that article title 
might think it's about how to swap out a reference graph, or about something to
do with pointers, etc. Even someone carefully reading to figure out how to
modify a GBWT's path senses might miss this article. It lacks "GBWT", "path", 
"sense", etc.

More explanation on the wiki landing page would help. Even a sentence-long blurb 
about each article would help. Or the page could be shorter, simply pointing to 
other subpages about groups of articles. Anything but this vague list of titles.

---

We *are* trying to improve this documentation, especially the wiki's front page.
But I don't think these problems are unique to us. (Indeed, all of the posts in
[this series][CritiqueTag] are intended to showcase specific examples of common
problems.) For other folks who maintain complex workhorse toolkits: the very
best of luck to you. Also, if you have ideas, shoot me an email. Address in my
[CV][CV].

---

1. Hi, that's me. I've been both within the past year. Though I'm at least past
the major hump now; I have decent familiarity with at least which functionality 
is in which commands. That's due to extensive use. Also because I'm nosy and 
poked my head into [literally every subcommand's code][CheckOptionsPR].
2. Also, this is sort of a to-do list for me. Improving the wiki landing page is
next up on the list of side projects.
3. [Quote][DeadlineQuote] from Chapter 15 of *Project Hail Mary* by Andy Weir
    > “Not know. Many things break. My people make ship very hurry. No time to
    > make sure all things work good.” Deadline-induced quality issues: a
    > problem all over the galaxy. 

    This post started off as a musing about writing code under deadlines and was
    going to include that quote. I really love *Project Hail Mary*, see. I love
    it an incorrect amount. As in, I've listened to the audiobook upwards of
    thirty times. So I needed an excuse to put this quote in anyhow.

[ChangingRefWiki]: https://github.com/vgteam/vg/wiki/Changing-References
[CheckOptionsPR]: https://github.com/vgteam/vg/pull/4654
[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[CV]: https://faithokamoto.github.io/cv/
[DeadlineQuote]: https://www.reddit.com/r/ProjectHailMary/comments/1bbvrl2/deadlineinduced_quality_issues_sad_sad_sad/
[DocumentationTag]: https://faithokamoto.github.io/tags/#documentation
[FilterPR]: https://github.com/vgteam/vg/pull/4234
[FilterWiki]: https://github.com/vgteam/vg/wiki/Getting-alignment-statistics-with-vg-filter
[ManpageIssue]: https://github.com/vgteam/vg/issues/4700
[SearchResults]: https://duckduckgo.com/?t=ffab&q=site%253Afaithokamoto.github.io%252F+vg&ia=web
[vgGitHub]: https://github.com/vgteam/vg
[vgManpage]: https://github.com/vgteam/vg/wiki/vg-manpage
[vgREADME]: https://github.com/vgteam/vg/blob/master/README.md
[vgWiki]: https://github.com/vgteam/vg/wiki
[WholeGenomeWiki]: https://github.com/vgteam/vg/wiki/Working-with-a-whole-genome-variation-graph/2f5afeab59ef6c06f990e08ce71eed09e97868c7