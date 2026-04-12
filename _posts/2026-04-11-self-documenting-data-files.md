---
layout: post
title: Self-documenting data files
subtitle: Not just code should be usable
tags: [data, self-documenting]
author: Faith Okamoto
---

I recently achieved that unicorn of collaborative science code: I passed off a
section of my work to someone who'd never touched it before, and she figured it
out without more than me just pointing her at my files. Thus, I thought I should
write about a key component of that success.

----

## "Self-documenting data files"?

I've previously covered the concept of self-documenting _code_ (i.e. code that
can be easily read), but what do I mean by a self-documenting _data_ file?
Basically the same thing: a file whose structure and function is immediately
obvious just by looking at it.

Look at the following two examples:

- `counts.csv`
    ```
    M001,22
    F001,21
    M002,34
    ```
- `2026_04_11_polyp_counts.csv`
    ```
    rat,polyps
    M001,22
    F001,21
    M002,34
    ```

Same data, but one is much more usable. The main important element is the
presence of header information. Raw values aren't much use if we don't know what
they are! The header I added here is relatively simple; see other formats such
as [VCF][VCF] for more complex headers.

For logfiles, this might mean adding context words around prints. For example,
"Selected haplotype HG002.1 with score 9422" is much more useful to a later
reader than "HG002.1 9422", though the raw information content is the same.

Essentially, ask yourself: could someone without my context understand what
information is being presented here? If so, great! If no, how can you fix that?

## When is this needed?

Well, in my case I was handing a data file to someone else so they could make
plots with it. Being self-documenting was very useful for this purpose. She
didn't have to ask me which parts of the file she should use; instead she just
read the column headers and decided what information she wanted.

Of course, sometimes this header stuff can be unnecessarily difficult. If I'm
double-checking some lines and happen to dump them into a file, then I'm 
probably not going to bother slapping a header on whatever `awk` coughs up. The
key is simply whether this file will be used again. If so, make at least some
effort to document it. If not, delete it. If you're wary about deleting it, then
think about going back to step one instead.

----

Short one today, I know, but I'm just trying to evangelize the basic practice
of, for the love of all that is good, making _readable_ data files. Thank you
for coming to my TED talk :)


[VCF]: https://samtools.github.io/hts-specs/VCFv4.2.pdf