---
layout: post
title: Take out the leftovers
subtitle: (if they're candy give them to me)
tags: [published-code-critique, last-pass]
author: Faith Okamoto
---

I'm one of the people who has to present a paper at my lab's next journal club.
Therefore, I'm going to check in on the code for the one we chose.

This month's paper: Romain, S *et al*. Representation and detection of inversions 
in pangenome graphs. *NAR Genomics and Bioinformatics* 2026. doi:
[10.1093/nargab/lqag125][DOI]

## Original code

The scripts for this paper are on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Commit to comments

[`00_extract_multifasta_from_agc.py`][Script00]:

```py
#
paths: list = list()
with open('temp.txt', 'r', encoding='utf-8') as reader:
    for line in reader:
        paths.append(line.strip()[:-2])
```

I'm not leaving anything out. That is just an empty comment.

This section is fairly self-explanatory as to what it's doing (except that I'm
unsure why the last two fields are being cut off), so I wouldn't have been 
surprised if there was no comment. However, if there's going to be a comment, 
leaving it empty does nothing but cause confusion. I pause and wonder if there's 
invisible text or part of the code isn't loading or similar.

### Remove unused code

[`01_ragtag_chrom_contig_assoc.sh`][Script01]:

```sh
# Filter chromosomes to use from reference genomes
cd $OUTDIR
chrom_to_exclude="ragtag_exclude_extra.txt"
#grep '^>' $REFERENCE | awk '{ print $1 }' | sed -r 's/>//g' | grep -F '_' > $chrom_to_exclude
#echo 'chrEBV' >> $chrom_to_exclude
echo 'chrmitochondrion' > $chrom_to_exclude
```

From the looks of it, those two commented-out lines were previous things that
were being used but are no longer. Leaving them in is odd. If there's something
useful there (e.g. maybe that logic should be used in some cases), then that
should be explained, probably by another comment. Or if those are simply old
versions that are no longer needed, then best would be to delete them, instead
of having them hang around ghosting into the reader's working memory.

### Use spellcheck

At least on [README][README]s, maybe?

> Script: `03_extract_select_contigs.sh`
> Lists each haplotypes contigs conrresponding to a given chromosome, then extracts them using samtools faidx.

There shouldn't be an "n" before the "r"s in "corresponding".

I know that it's not practical to run spellcheck on code files (the red squiggly 
lines for my C++ code would give me a conniption), and I know that I typo often. 
Still. READMEs are meant to be read by other people. One kindness you can do for
those other people is making sure things are spelled correctly.

For example, I spellcheck these blog posts by copy-pasting a first draft into a
browser tab (https://rot13.com/ to be specific, since it's a perfect no-frills
ad-free textbox) and letting the automatic spellcheck there do its magic. It's
very quick for me to glance through all the possible errors and dismiss false 
positives. I catch typos nearly every time I do this.

----

The common thread between all of these is that it can really pay off to do one
final run-through of anything you provide to other people, just to wash off the
artifacts which may have ceased to matter to you but would matter to them.

If there's a recent paper you'd like me to look through, shoot me an email. 
Address in my [CV][CV].

[Code]: https://github.com/SandraLouise/INVPG_annot_paper
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1093/nargab/lqag125
[README]: https://github.com/SandraLouise/INVPG_annot_paper/blob/main/data/HUMAN/README.md
[Script00]: https://github.com/SandraLouise/INVPG_annot_paper/blob/main/data/HUMAN/00_extract_multifasta_from_agc.py
[Script01]: https://github.com/SandraLouise/INVPG_annot_paper/blob/main/data/HUMAN/01_ragtag_chrom_contig_assoc.sh