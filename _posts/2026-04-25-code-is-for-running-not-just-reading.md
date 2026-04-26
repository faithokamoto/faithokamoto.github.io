---
layout: post
title: Code is for running, not just reading
subtitle: (though reading is important)
tags: [published-code-critique, runnable]
author: Faith Okamoto
---

I usually start my [published code critiques][CritiqueTag] by copying the
previous post, just to get the formatting, which means I'm now noticing that
last month's critique was after the first time I watched *Project Hail Mary*.
I've now watched it thrice. You may not have guessed that this bioinformatics 
PhD student who blogs about scientific coding practices is a bit of a nerd, 
but indeed, I am.<sup>1</sup>

At work, while listening to the soundtrack on repeat, this week it was my turn to
co-lead journal club. Might as well look at the code for their paper.

This month's paper: Cousins T *et al*. Deep coalescent history of the hominin 
lineage. *bioRxiv* 2026. doi: [10.1101/2024.10.17.618932][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Agh, absolute file paths!

There is a time and a place to put absolute file paths in your public code. That
time is not here:

```python
configfile: "/home/tc557/T2T_PSMC/T2Tsequences/260127snakefile/config.yaml"
```

This Snakemake file has a config path. Fine, that's an important part of a
snakefile. But the filepath requires access to the original computer. How am I
the external interested scientist supposed to know what's in that file?

It's also frustrating that this is a completely unforced error. The config file
(or what I really hope is the config file) is [in the repository][Config] 
already. If that is actually the config file then the reference could simply be
swapped for a relative filepath. But with what's currently there, I can't be
sure what the exact config is. And that's an issue for reproducibility.

### Over-specific shebang

Vocab time: a ["shebang"][Shebang] is that line at the top of a file which tells
the computer how to run it. That was probably confusing. Basically, you can
start `script.sh` with

```sh
#!/bin/bash
```

and when you run `./script.sh` then it will be executed with the Bash shell.

Anyhow. That is lead-up to explain why this is Bad:

```
#!/home/tc557/miniconda3/envs/snakemake_new/bin/python
```

This is telling the computer to use Python from a particular conda environment. 
Within a specific home directory structure. Who else could run this?

If this just means the Python for this repository's environment<sup>2</sup>, 
there are better ways. `#!/usr/bin/env python3` is my standard Python shebang. 
That will actually look up the Python within the current environment.

### Snakefiles can have relative paths

The snakefiles in here have, for example,

```python
rule run_MSMC2_1KGP:
    input:
        mhsfiles = get_mhs_files,
    output:
        outfile = '/home/tc557/rds/hpc-work/MSMC2_1KGP/inference260221_alignedtoHG002/MSCM2/D_{D}/iterations_{iterations}/theta_{theta}/rhoovermu_{rhoovermu}/{sample}_m{m}_sdust{sdust_w}.{sdust_t}.final.txt',
        outlog = '/home/tc557/rds/hpc-work/MSMC2_1KGP/inference260221_alignedtoHG002/MSCM2/D_{D}/iterations_{iterations}/theta_{theta}/rhoovermu_{rhoovermu}/{sample}_m{m}_sdust{sdust_w}.{sdust_t}.log',
```

While this might make most sense if only one person will ever run this analysis,
I don't really think that's the case here. The whole process is conceptually
simple enough that it would make a nice starter reproduction assignment for an
undergrad/trainee. Yet, they'd have to fight the snakefile first.

You can use relative path stuff in a snakefile. The [lab one I use][LRGsnake]
has... a lot... of issues, but at least it writes everything to a "root"
directory that is just where the repository is located. That way I can run it
within my own directory instead of worrying about writing to someone else's.

----

In general, you should be asking: can someone run these files if they aren't me?
The code here is relatively nicely documented and readable. But that means much
less if it's not _runnable_.

Kill absolute paths with fire. Please.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

----

1. *The Martian* reference. I'm re-reading it for some friends right now.
2. Also, if this is supposed to be a conda environment, then... that's not
documented in the README. Just sayin'. I can guess it from the runnable notebook
but that's decidedly non-ideal. This doesn't get its own section because I try
to avoid repeating myself. It just gets this increasingly long ramble note.

[Code]: https://github.com/trevorcousins/twin_peaks
[Config]: https://github.com/trevorcousins/twin_peaks/blob/main/config.yaml
[CV]: https://faithokamoto.github.io/cv/
[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[DOI]: https://doi.org/10.1101/2024.10.17.618932
[LRGsnake]: https://github.com/vgteam/long-read-giraffe-experiments/blob/main/Snakefile
[Shebang]: https://en.wikipedia.org/wiki/Shebang_%28Unix%29
[Tests]: https://github.com/albertjimenezbl/theseus-lib/tree/main/tests