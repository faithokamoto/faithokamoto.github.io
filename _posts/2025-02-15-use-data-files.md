---
layout: post
title: Use data files
subtitle: February 2025
tags: [published-code-critique, documentation, naming]
author: Faith Okamoto
---

I'm not making this whole blog into critiques. My February is just busy, and I
don't want to run out of time for this month's critique.

This month's paper: 
Duran JA *et al.*. Genetic resonance: dissecting the heritability and genetic correlations of human hearing acuity. *G3 Genes|Genomes|Genetics* 2025. doi:
[10.1093/g3journal/jkae292][DOI]

## Original code

Code files [were released][DataAvailability] as [RMarkdown][RMarkdown] files on
[GitHub][Code]. This is great [reproducibility][ReproduceBlog] since I should be
able to run the R Markdown and get the same results.

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Don't hard-code data into code files

The first thing I noticed was hard-coded data. In `Narrow-sense CLs.Rmd`:

```r
# Define the data and reverse the order of frequencies
solar_data <- data.frame(
  Frequency = factor(c(250, 500, 1000, 2000, 3000, 4000, 6000, 8000, "PTA", "HFA"), 
                     levels = rev(c(250, 500, 1000, 2000, 3000, 4000, 6000, 8000, "PTA", "HFA"))),
  Narrow_sense = c(0.51, 0.45, 0.36, 0.56, 0.35, 0.28, 0.36, 0.30, 0.50, 0.37),
  S.E. = c(0.07, 0.07, 0.08, 0.08, 0.09, 0.09, 0.10, 0.07, 0.07, 0.09)
)
```

Please, don't do this. It's hard to tell which values correspond to each other
at a glance. Plus, exporting this table for use elsewhere is annoying. Such
problems multiply for larger data tables.

Since it's quite long, I won't copy it here, but several of the code files use
the exact same data table, hard-coded in separately each time. It would be much
better to **put the data in a file**, uploaded along with the code. Then it can
be loaded in one line each time it is used. No copy-paste errors either.

### Break up scripts into separate components

Using the technical meaning of ["critique"][Critique], this section is actually
praise. The code is well split up into conceptually singular snippets. For
example, that `Narrow-sense CLs.Rmd` file does these things:

1. Load requirements (`ggplot2`, hard-coded data)
2. Calculate confidence limits for two variables
3. Create a specific plot
4. Display that plot

This follows a logical progression with no detours. If someone wanted to know
how that plot was made, pointing them to this script would be a great answer.

However, there are some considerations when breaking up scripts. One of those,
probably behind the copy-pasted hard-coded data, is multiple analyses relying on
the same set-up. One method is to put each sub-analysis in a file and then copy 
along everything necessary for it, which seems to be the method used here.
Better to factor out the shared component into a data/helper file.

### Provide directions on running files

The GitHub repository has various R Markdown files as well as some command-line
scripting. If I wanted to reproduce the analysis, it's great to have all the
code in one place (and the comments are pretty good) but it would be even better
to know exactly what to run and when. I recommend putting instructions in a
README or similar. Literally, a [list of steps to reproduce][ReproduceBlog].

Enough thinking and cross-referencing with the paper would probably let me
figure out how to use the code. But I'd rather not guess.

----

This paper definitely has some of the better science code I've seen out there.
But there's always room for improvement.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[CV]: https://faithokamoto.github.io/cv/
[Code]: https://github.com/FishingNerd/hearing_acuity
[Critique]: https://www.britannica.com/dictionary/critique
[DataAvailability]: https://academic.oup.com/g3journal/article/15/2/jkae292/7921919#502820597
[DOI]: https://doi.org/10.1093/g3journal/jkae292
[ReproduceBlog]: https://faithokamoto.github.io/2025-01-25-reproduce-your-work/
[RMarkdown]: https://rmarkdown.rstudio.com/