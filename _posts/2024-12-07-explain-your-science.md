---
layout: post
title: Explain your science
subtitle: Including your assumptions
tags: [comments, science-meaning]
author: Faith Okamoto
---

Science code, at least theoretically, represents something tangible. Modeling
the spread of a virus in simulated populations. Parsing gads of sensor output
for peaks of relevant data. Graphing statistics on tests taken across a country.
Because we deal with stuff that has concrete meaning, concrete and defensible
constraints crop up often. Often those constraints end up in code. When they do,
they should be explained.

## What science?

When we write science code, it comes with implicit assumptions. You should make
these assumptions explicit. Some examples from my recent experience:
* [Hi-C][HiC] read mates which map to different chromosomes can be ignored. 
(There aren't very many of them due to how the Hi-C procedure works.)
* Genotype frequencies generally follow [Hardy-Weinberg equilibrium][HWE].
* Exons are transcribed in base-pair order, regardless of human-assigned exon
numbers. (This is how [RNA polymerase II does transcription][Transcription].)

If you didn't know the science behind my code, it might seem I'm arbitrarily
discarding a bunch of useful data, making up equations out of thin air, or
relying on unfounded assumptions. These are restrictions founded in science, not
pure programming necessity.

## Why explain the science?

It's important to explain these "arbitrary" restrictions for two main reasons.
1. Readers will understand what the code is doing and why.
2. Inconsistencies between the science and the code are easier to spot.

The first is standard fare for me. (See [my tags][Tags]...) I'll expand on #2.

Let's use my third bullet point as an example. The `vg rna` command is supposed
to [add edges representing splice junctions to a pangenome graph][VGRNA]. It
parses a [GFF3][GFF3] file to know where the exons are. Originally, it validated
that the exons of each transcript were in order by comparing their exon number
(a tag in the GFF3) to the number of exons parsed so far for that transcript.
In other words, it **assumed exon numbers increased down the file**.

This assumption about exon numbering was not made explicit when `vg rna` warned
about exons supposedly being out of order. I was baffled when all of my GFF3's
[reverse-strand genes][ReverseStrand] were dropped. While my exons were sorted
by base-pair position, they were numbered in order of transcription. That is,
**for reverse strand genes, exon numbers decreased down the file**.

Now, whether humans want to number the exons forward or backwards doesn't matter
for **the scientific concept represented by the program**. Recall this is just
splice junctions. An edge, connecting two exons as adjacent for RNA-seq, doesn't
care about the numbers. It cares about which exons are physically adjacent.

So I [made a pull request][PullRequest] to change the "out of order" logic to
rely on exon positions instead of their numbers. It would've been a lot easier
to figure out the problem if the old science assumption was explicit, but at
least now my science assumption is explicit.

Your code can work as intended but still be wrong, if the intention itself is
wrong. Your code can also be broken but have the right intent, but that sort of
discrepancy is easier to catch. Either way, explaining the underlying science is
a service to all.

[GFF3]: https://github.com/The-Sequence-Ontology/Specifications/blob/master/gff3.md
[HiC]: https://doi.org/10.1016/j.ymeth.2012.05.001
[HWE]: https://www.nature.com/scitable/knowledge/library/the-hardy-weinberg-principle-13235724/
[PullRequest]: https://github.com/vgteam/vg/pull/4471
[ReverseStrand]: https://biology.stackexchange.com/q/110516
[Tags]: https://faithokamoto.github.io/tags/#comments
[Transcription]: https://www.khanacademy.org/science/biology/gene-expression-central-dogma/transcription-of-dna-into-rna/a/stages-of-transcription
[VGRNA]: https://github.com/vgteam/vg/wiki/Transcriptomic-analyses