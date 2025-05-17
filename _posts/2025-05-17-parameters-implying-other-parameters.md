---
layout: post
title: Parameters implying other parameters
subtitle: But what does that mean?
tags: [parameters, errors]
author: Faith Okamoto
---

Some options are meant to be used together. This might be bidirectional (e.g.
both a sample name and a data file) or it might be one-way (e.g. an alignment
file needs a genome file, but not the other way around). In either case, using a 
specific optional argument requires the use of another "optional" argument.

## Documenting implications

Wherever the arguments are documented, be clear that using one implies another.
For example, from [vg giraffe][GiraffeMain]:

```
  --track-provenance            track how internal intermediate alignment candidates were arrived at
  --track-correctness           track if internal intermediate alignment candidates are correct (implies --track-provenance)
  --track-position              coarsely track linear reference positions of good intermediate alignment candidates (implies --track-provenance)" 
```

This removes surprises. I know that if I pass `--track-correctness` then the
`--track-provenance` functionality will occur. Alternatively, this information
could go in a docstring:

```python
def filter(alignments, min_mapping_quality, chromosome=None, position=None):
  """Filter alignments for a minimum mapping quality score.

  [...]

  chromosome : str, optional
    Only use alignments to this chromosome.
  position : tuple, optional
    Only use alignments within this range of positions
    (requires "chromosome" to be set)
  """
```

Here, instead of another option being applied automatically, the code requires
`chromosome` to be manually set alongside `position`.

## Incorrect usage

But what happens if the user *doesn't* follow these guidelines? Either they
disregarded the instructions, or there weren't any warnings at all. What now?

Best option? A program failure. Ideally with an error message such as "the 
`position` argument requires `chromosome` to be set". By getting this kind of
[useful error message][ErrorMessages], the user can easily fix their code.

That last paragraph seems sort of obvious, right? But it's not always done. More
times than I care to count, I've had to debug errors that came from my misuse of
arguments which depended on each other, where my error messages were unhelpful
at best. Or the program worked but the output wasn't what I expected.

As a practical example, take another tool from vg, the transcriptome graph maker
[`vg rna`][RNAMain]. It takes a graph and a list of gene annotations, then
modifies the graph to add edges connecting exons. There's an option to "project"
these annotations onto haplotypes other than the one in the annotation file.
Then there is a *separate* option to save those annotations in the graph. These
options are rather clearly meant to be used together. Using the former but not
the latter is almost certainly a user error. Yet, doing so causes no error. It
makes the tool do a bunch of computations to project annotations, but then
throws away all of that work, since the user didn't ask to save it in the graph.

Don't be like that. Warn your user about what they're doing.

## Why is this hard?

In a deviation from my normal posts where I just recommend what to do, here I'll
speculate on why this recommendation is even required.

Put simply, cataloguing your own assumptions is hard. *You* know how this code
is intended to be used. You wouldn't make these sort of overlooking errors.
You'd never invoke that function with only one of the paired arguments. The
issue is that users don't know what is obviously wrong. Even if the issue is
obvious from a single glance by the developer, ideally the end user would fix
their own issue before it ever got to that state.

So: idiot-test your stuff. Think through all the wrong ways it could be used.
Even the idiotic ones. *Especially* the idiotic ones. Then make sure there are
useful error messages where needed. Help your users help themselves. Everyone
messes up. The key is knowing when you have.

[ErrorMessages]: https://faithokamoto.github.io/2025-01-10-useful-error-messages/
[GiraffeMain]: https://github.com/vgteam/vg/blob/61cfb60bb4963b9f378ebcf2babe240b1e0a6a33/src/subcommand/giraffe_main.cpp#L776
[RNAMain]: https://github.com/vgteam/vg/blob/master/src/subcommand/rna_main.cpp