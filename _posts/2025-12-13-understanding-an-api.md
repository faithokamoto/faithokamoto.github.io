---
layout: post
title: Understanding an API
subtitle: December 2025
tags: [published-code-critique, documentation, comments]
author: Faith Okamoto
---

It's the holidays and I just needed to find some article to write about. So I'm
going with the marker paper for minimap2. It's a hugely important tool in my
field but I don't think I've ever looked at its code.

This month's paper: Li H. Minimap2: pairwise alignment for nucleotide sequences. 
*Bioinformatics* 2024. doi: [10.1093/bioinformatics/bty191][DOI]

## Original code

This paper's code is on [GitHub][Code]. I focus on [`minimap.h`][Header]
because it is supposed to document the API.

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### What options does this field have?

First off, let's explain "[API][API]". It stands for Application Programming
Interface: if you're programming an application of this code, then here's the
interface to use. Any functions exported by the package/tool/etc. should have
their inputs and outputs documented. What happens behind the scenes isn't the
user's problem; the back-end implementation may change, but the API should be
relatively constant for ease of use.

Thus, it's pretty important for the elements of an API to have documentation. If
I don't know what the inputs to a function are, then I can't be sure how to use
it. For example, an early [struct][StructsBlog] is:

```c
// minimap2 index
typedef struct {
	char *name;      // name of the db sequence
	uint64_t offset; // offset in mm_idx_t::S
	uint32_t len;    // length
	uint32_t is_alt;
} mm_idx_seq_t;
```

Setting aside that `is_alt` would make more sense as a boolean, what values can
it take on? If I make a `mm_idx_seq_t` which is or is not an alt, should it be 1
and 0? Max value and 0? Something else? If I write a function which accepts
`mm_idx_seq_t`s, what values do I need to be able to handle?

While this information may be elsewhere, it would be most useful to at least
have a pointer around where the struct is defined, as that is where a user will
most likely look first.

### Abbreviations are not always obvious

Another struct is:

```c
typedef struct {
	int32_t id;             // ID for internal uses (see also parent below)
	int32_t cnt;            // number of minimizers; if on the reverse strand
	int32_t rid;            // reference index; if this is an alignment from inversion rescue
	int32_t score;          // DP alignment score
	int32_t qs, qe, rs, re; // query start and end; reference start and end
	int32_t parent, subsc;  // parent==id if primary; best alternate mapping score
	int32_t as;             // offset in the a[] array (for internal uses only)
	int32_t mlen, blen;     // seeded exact match length; seeded alignment block length
	int32_t n_sub;          // number of suboptimal mappings
	int32_t score0;         // initial chaining score (before chain merging/spliting)
	uint32_t mapq:8, split:2, rev:1, inv:1, sam_pri:1, proper_frag:1, pe_thru:1, seg_split:1, seg_id:8, split_inv:1, is_alt:1, strand_retained:1, is_spliced:1, dummy:4;
	uint32_t hash;
	float div;
	mm_extra_t *p;
} mm_reg1_t;
```

The fields with comments I can at least figure out what the abbreviation stands
for. It's clear `cnt` = "count", for example. But I'm not sure what `div` is
("divisor"? "division"?). Worse, I have no idea what `reg1` is short for. What
does this struct represent in general? I understand giving things shortened
names for ease of programming. But at least stick a [docstring][DocstringsTag]
up so an API user has a quick reference for what each thing is.

### When offering options, explain the difference

There are a few similar functions here:

```c
int mm_max_spsc_bonus(const mm_mapopt_t *mo);
int32_t mm_idx_spsc_read(mm_idx_t *idx, const char *fn, int32_t max_sc);
int32_t mm_idx_spsc_read2(mm_idx_t *idx, const char *fn, int32_t max_sc, float scale);
int64_t mm_idx_spsc_get(const mm_idx_t *db, int32_t cid, int64_t st0, int64_t en0, int32_t rev, uint8_t *sc);
```

When do I use one over another? They clearly have related names; two differ by
only a single character, yet have different arguments. Remember that the point
of an API is to let an end-user put in inputs and get outputs without worrying
over implementation. As it stands, I have no idea what the inputs are, which
function should be used for what, or what output to expect. That makes this part
of the API less useful than it should be.

---

It's great to offer a clean API for downstream users. But it's even better to
document that API well enough for even more ease of use.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[API]: https://en.wikipedia.org/wiki/API
[Code]: https://github.com/lh3/minimap2
[CV]: https://faithokamoto.github.io/cv/
[DocstringsTag]: https://faithokamoto.github.io/tags/#docstrings
[DOI]: https://doi.org/10.1093/bioinformatics/bty191
[Header]: https://github.com/lh3/minimap2/blob/master/minimap.h
[StructsBlog]: https://faithokamoto.github.io/2025-06-07-using-simple-structs/