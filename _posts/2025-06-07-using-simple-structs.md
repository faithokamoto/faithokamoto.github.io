---
layout: post
title: Using simple structs
subtitle: Name all the things!
tags: [naming]
author: Faith Okamoto
---

The last assignment for my [class on plotting][Plots] required sophisticated
data processing and storage. My storage method of choice was a simple struct.

----

## What's a struct?

That [terminology is from C][Struct]. In Python it's a [dataclass][Dataclass]. 
I think these make most sense by example, thus:

```python
@dataclass
class Region:
    """Data class to hold genomic region information."""
    chrom: str
    start: int
    end: int

# Instantiate
region = Region(chrom, start, end)
# Access
print(region.chrom)

@dataclass
class Annotation:
    """Data class to hold block information."""
    begin: int
    end: int
    # Blocks to plot
    starts: list
    widths: list
    heights: list
    y: float = None

# Note that no "y" value is passed; it will have the default of None
annot = Annotation(cur_region.start, cur_region.end, 
                   block_starts, block_widths, heights)
```

Essentially, a struct is in between a tuple and a regular class. Its primary 
purpose is to store a few bits of data. Each attribute has a name and can have 
a default. The struct class itself can have simple methods (not shown).

The main distinction from a [`NamedTuple`][NamedTuple] is increased flexibility.
The values are mutable, after all! A struct is also distinct from a list/vector
or similar data structure: it has a fixed number of fields of fixed type.

## Why use structs?

Okay, so I showed you a shiny way of organizing data. Why should you care?

Because (say it with me now) *readability*! Many of my classmates used lists to
store the same information. That meant no attribute names. A pain to debug. If 
you access index `3`, or index `-1`, what exactly is stored there? I had to go
back and check their declaration every time. In contrast, in my code I simply
accessed attributes by name.

Python's dataclasses also have the major quality-of-life conveniences of a 
default constructor (the attributes, in order) and a default method to convert 
to a string (the attributes, labeled, in order). Creating and debugging my 
structs was quick and easy without having to write boilerplate.

---

This is one of my pieces that I'm absolutely sure someone else must've written
already. But perhaps now you can look at your code and see if anything can be
refactored into a struct. For readability and beyond!

[Dataclass]: https://docs.python.org/3/library/dataclasses.html
[NamedTuple]: https://docs.python.org/3/library/typing.html#typing.NamedTuple
[Plots]: https://faithokamoto.github.io/2025-04-05-magic-numbers-in-plotting/
[Struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)