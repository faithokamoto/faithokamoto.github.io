---
layout: post
title: Magic numbers in plotting
subtitle: Abracadabra, make a graph!
tags: [style, plots]
author: Faith Okamoto
---

I've just started a [class on making scientific plots][BME263] so I'll cover
a common phenomenon: [magic numbers][MagicNumbers].

## What's a magic number?

I use this definition: **A _magic number_ is a hard-coded non-obvious value**.
Notably, "value" includes non-numbers such as strings.

* **Hard-coded**: A value appearing directly in the source code. For example, in
`len(read) > 200` and `geno = '0|1'`, `200` and `'0|1'` are magic numbers.
* **Non-obvious**: The reason for this *specific* value is not obvious from the
statement itself. Often 0 and 1 have obvious reasons, such as `colors[0]` or
`for i in range(1, k+1)`.

My usual rule of thumb is to check for any hardcoded value that *isn't* 0 or 1,
and then consider each of those on a case-by-case basis.

## Why are magic numbers (usually) considered bad?

Magic numbers are problematic due to readability. Plus they commonly violate
[DRY][DRYBlog]. For example, consider the following code which checks each
alignment for quality and then tries to "rescue" the poor-quality ones:

```python
if alignment.quality() < 10:
    poor_quality_alignments += 1
    # ...
    # 20 lines of trying to rescue alignment
    # ...
    if rescued_alignment.quality() >= 10:
        rescued_alignments += 1
        alignment = rescued_alignment
```

Here, the `+= 1` bits aren't magic numbers. It's obvious they're incrementing
counters. However, the quality threshold *is* a magic number: why isn't it
higher or lower? Is it intentional that the same threshold is used both times? A
refactored version would be:

```python
QUALITY_THRESHOLD = 10
if alignment.quality() < QUALITY_THRESHOLD:
    poor_quality_alignments += 1
    # ...
    # 20 lines of trying to rescue alignment
    # ...
    if rescued_alignment.quality() >= QUALITY_THRESHOLD:
        rescued_alignments += 1
        alignment = rescued_alignment
```

This code is more readable. Plus, it's easy to change the threshold later.

## So what about plots?

Plots and magic numbers are... tricky.

Technically plotting tends to involve a whole bunch of magic numbers. Figure
sizes, panel sizes, axes limits, axes labels, legend position, the exact
location of that one arrow you've been trying to get in place for ages, etc.

But unlike regular coding, I actually don't recommend getting out the pitchforks
here. Titles quite often make most sense simply hardcoded within a plot, in
their native context. The Y-value of a horizontal line should probably be
hardcoded in the horizontal-line function call. And for goodness' sake, just
put the legend's position label within the legend-making function call itself.

In plotting, magic numbers are a necessary evil.

However, that doesn't mean you shouldn't factor out *any* magic numbers. 
Personally, when plotting, I factor out magic numbers I use more than once. If I
have the same X-axis label in multiple plots, I make it a variable. If I place
panels relative to a larger figure, it probably makes sense to factor out the
larger figure's dimensions into variables. Especially in a plotting context,
it's useful to know when two values are the same on purpose.

[BME263]: https://courses.engineering.ucsc.edu/courses/bme263
[DRYBlog]: https://faithokamoto.github.io/2025-03-14-dont-repeat-yourself/
[MagicNumbers]: https://stackoverflow.com/questions/47882/what-are-magic-numbers-and-why-do-some-consider-them-bad