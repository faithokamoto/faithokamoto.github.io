---
layout: post
title: Reading some tests
subtitle: lovely yummy unit tests
tags: [published-code-critique, testing]
author: Faith Okamoto
---

I just watched *Project Hail Mary*, the movie adaptation of a book that I have
literally listened to over thirty times, and I'm still a bit giddy. I've even 
mentioned my love for the novel [on this blog][MegaToolsBlog] before.

But I guess I should write an actual blog post, not an ad. So here's a paper
where we (as in vg team) are actually trying to work with the authors. Thus
it would behoove me to have a better idea of what they're doing.

This month's paper: Jiménez-Blanco A *et al*. Theseus: Fast and Optimal 
Affine-Gap Sequence-to-Graph Alignment. *bioRxiv* 2026. 
doi: [10.64898/2026.02.12.705572][DOI]

## Original code

This paper's code is on [GitHub][Code]. I'll specifically be focusing on the
[unit tests][Tests], mostly because I thought it nice they were there.

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### How do I run the tests?

So, I found these tests. But I'm not clear how I would actually run them. There
isn't any mention in the README. (Come to think of it, there isn't a mention in
the vg README either. I should make a PR...) If I set up a Theseus instance,
what command makes it use its testing files?

How to use the tests is probably obvious to the developer who wrote those tests.
However, tests aren't only for the original developer. They're also useful for
folks who are extending old code, verifying that a function works how it works,
or who simply want to see a small example in action.

Just an example command to run a particular test would really work wonders.

## Shouldn't there be more tests?

The unit tests are in three files based on the functionality they test. Since
[`seq_to_graph_tests.cpp`][seqtographtests] seemed relevant to me, I clicked on 
it first, only to be rather disappointed.

The entire file has exactly one test. This test runs exactly one subcase. It
has a single graph and a few sequences, then tests that the sequences align
correctly against the graph. The graph _is_ somewhat interesting, as it has a
cycle (a rather difficult structure for aligners), but it is, again, just one
graph. What about graphs without cycles? If nothing else, having that sort of
test case would disambiguate "broke the aligner entirely" errors from "broke the
cycle handling" errors.

In general, having an array of test cases, handling a few notably different 
inputs, is important to be more confident that the code is working correctly.
If you test one graph, then you can be confident that exactly one graph works.
What about nested cycles? What about inversions? What about graphs where the
sequences [should align backwards][ReversalIssue]? And beyond just what *you*
the developer can think of, there are other tricky cases. A random test case is 
useful to find unexpected problems. Remember, anyone can make an algorithm that 
they themself can't break. The trick is making one that no one else can break.

## Explicit test names are useful

This section is actually praise. The subcases of [`msa_tests.cpp`][msatests] are
quite nice. Each is explicit about what exactly it tests. "Correct MSA with a
matching sequence" tests... if the MSA is correct for a pair of identical
sequences. Ditto for "Correct MSA with a sequence with a mismatch", etc.

These names act as comment/section headers, guiding the reader to know what the
next bit is about. As a bonus, when the test fails, its name is presumably
given, which means that you'd get an immediate explanation for what broke.

Yay! Naming! If I sound like a broken record, then that's because I am :D

----

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/albertjimenezbl/theseus-lib
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.64898/2026.02.12.705572 
[MegaToolsBlog]: https://faithokamoto.github.io/2025-09-22-documentation-and-mega-tools/
[msatests]: https://github.com/albertjimenezbl/theseus-lib/blob/main/tests/unit/msa_tests.cpp
[ReversalIssue]: https://github.com/albertjimenezbl/theseus-lib/issues/1
[seqtographtests]: https://github.com/albertjimenezbl/theseus-lib/blob/main/tests/unit/seq_to_graph_tests.cpp
[Tests]: https://github.com/albertjimenezbl/theseus-lib/tree/main/tests