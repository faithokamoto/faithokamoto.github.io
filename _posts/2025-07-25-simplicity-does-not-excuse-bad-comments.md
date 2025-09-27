---
layout: post
title: Simplicity does not excuse bad comments
subtitle: July 2025
tags: [published-code-critique, comments]
author: Faith Okamoto
---

Usually the papers I review are published. But Heng Li recently put the most
beautiful paper on arXiv, and I wanted an excuse to read through it again.

This month's paper: Li H. Finding easy regions for short-read variant calling
from pangenome data. *arXiv* 2025. doi: [10.48550/arXiv.2507.03718][DOI]

(Seriously, this thing is beautiful. It's also short, if that helps.)

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Yay for human-readable summaries!

I'm about to critique bad comments, so it only seems fair to mention instances
of very useful comments. Both files in `scripts/` a section I would consider a 
[script docstring][ScriptDocstring]. In `scripts/gen-easy-401.mak` this is:

```make
# This Makefile is written for human472 *ONLY*
# which consists of 472 genomes including 354 chrX and 120 chrY
#
# This Makefile requires multiple input files you have to manually prepare.
# Most input files, except the BED file for pseudoautomsomal regions (PAR),
# can be generated from a reference FASTA and the ropebwt3 indices. The GRCh38
# section below shows the command lines. You additionally need to put bedtk,
# seqtk, bgzip and k8 on $PATH.
#
# run with "make -f thisFile.mak -j 8 build=hg38"
```

Wonderful! This is the first thing that catches my eye when I open the file,
and it tells me exactly what I'm looking for: what this thing is, what it
requires, and how to run it. For an end user who wants to run these scripts
themselves, these comments are quite useful.

That comment explanations are useful? Remember that. It'll come up.

### End-of-line comments should be *short*

Usually comments go on a line by themselves. But it's typically possible to
stick them at the end instead. This has the slight advantage of being extra 
clear which line the comment is about. However, because you're *adding* to a 
line, you might end up with a long line. A very, very long line.

Behold:
```make
ref_par=hg38.PAR.bed          # this is the only file that can't be generated from the reference or the pangenome
e2e_pan=hg38.472-k401.e2e.gz  # ropebwt3 fa2kmer -k401 -w10 hs38.fa | ropebwt3 sw --all -t64 -N100 human472.fmd - 2> hg38.472-k401.e2e.log | gzip > hg38.472-k401.e2e.gz
e2e_ref=hg38.hg38-k401.e2e.gz # ropebwt3 fa2kmer -k401 -w10 hs38.fa | ropebwt3 sw --all -t64 -N100 GRCh38.fmd - 2> hg38.hg38-k401.e2e.log | gzip > hg38.hg38-k401.e2e.gz
```

These comments, especially the latter two, are so long as to require either a
scrollbar or wrapping. A scrollbar isn't great, since then you lose sight of the
code line. Wrapping isn't great either. In either case, the mega-length comment
makes the line simply unwieldy.

I get that there isn't a great way to present anything as long as those
comments. But multi-line comments are always an option:

```make
# this is the only file that can't be generated
# from the reference or the pangenome
ref_par=hg38.PAR.bed
# ropebwt3 fa2kmer -k401 -w10 hs38.fa | \
#     ropebwt3 sw --all -t64 -N100 human472.fmd - \
#     2> hg38.472-k401.e2e.log | gzip > hg38.472-k401.e2e.gz
e2e_pan=hg38.472-k401.e2e.gz  
# ropebwt3 fa2kmer -k401 -w10 hs38.fa | \
#     ropebwt3 sw --all -t64 -N100 GRCh38.fmd - \
#     2> hg38.hg38-k401.e2e.log | gzip > hg38.hg38-k401.e2e.gz
e2e_ref=hg38.hg38-k401.e2e.gz 
```

Voila, now we can read everything at once.

### Um, what's happening here?

From lines 41 through 91, there are no comments at all. I'm left peering at
byzantine lines of code, trying to figure out what they're doing.

```make
.PHONY: all

all: $(prefix)a.easy.bed.gz $(prefix)b.easy.bed.gz

$(prefix).ref-gap.bed.gz:$(ref_fa)
	seqtk gap -l1 $< | bgzip > $@

$(prefix).ref-chr.bed:$(ref_fa)
	seqtk comp $< | awk '$$1~/^chr([0-9]+|[XY])$$/{print $$1"\t0\t"$$2}' > $@
```

What does `.PHONY: all` do? Why does one of these lines have an awk regex to
search for chromosome names, but the other doesn't? (For that matter, why is the
mitochrondrial chromosome not included?) Why are those parameters being used for
`seqtk`? What is is the purpose of any of this?

The rest of the script is more lines like those latter two. A march of chained
expressions, all somewhat similar but also somewhat different, sans any context
or explanation. Such explanations would be most useful if someone wanted to
run these scripts on another set of genomes.

These lines aren't *impossibly* complicated. I could probably peel them apart,
layer by layer, and figure out what each is doing. But simplicity isn't an
excuse to not explain. Middle-complexity code is the most dangerous thing to 
leave unexplained. It's easy for a reader to only *think* they understand.

So, [comments][CommentTag]. Comments are your friends, folks.

----

This paper still has really cool results, and the code isn't terrible. It's
relatively simple and well-formatted. Plus it has those script docstrings. I
just think the comments could use a little more love.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/lh3/panmask
[CommentTag]: https://faithokamoto.github.io/tags/#comments
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.48550/arXiv.2507.03718
[ScriptDocstring]: https://faithokamoto.github.io/2024-09-24-script-docstrings/