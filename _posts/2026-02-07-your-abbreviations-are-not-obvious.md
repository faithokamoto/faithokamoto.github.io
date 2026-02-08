---
layout: post
title: Your abbreviations are not obvious
subtitle: I am not a mindreader
tags: [published-code-critique, naming, comments]
author: Faith Okamoto
---

I'm nearly done with my thesis proposal first draft. Decided that I'd go back
and read the code for one of the papers I'm citing. Scanning through my list, I 
remembered that this one came out of the lab I would've been in, if my PhD was
at UC San Diego instead of Santa Cruz<sup>1</sup>.

This month's paper: Bzikadze AV and Pevzner PA. UniAligner: a parameter-free 
framework for fast sequence alignment. *Nature Methods* 2023. 
doi: [10.1038/s41592-023-01970-4][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Options should have more than a short-form version

There a quite a few Python scripts in here. I took a gander through the 
`tandem_aligner/py/utils` folder. These scripts use [argparse][argparse]. Which 
is great. It's a wonderful built-in library for command line interaction.

That's why I found [option set-up][comparecigars] so disappointing:

```py
def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("-i1", required=True)
    parser.add_argument("-i2", required=True)
    params = parser.parse_args()
```

Um. What are these? They seem to be somehow paired? One of the amazingly 
convenient things about argparse is the ease with which you can add helptext 
during set-up, which will be shown via `--help`/`-h`.

But running `--help` here wouldn't tell me what `i1` and `i2` stand for. What 
to guess? They're `i`nputs. A solution would be e.g. `--input-file-1` versions, 
along with a brief blurb explaining what to input.

The notation used here makes sense to the developer. It's even convenient. 
_They_ know that two input files are needed, and _they_ know what each one 
does. But I don't. **Readers are not mindreaders.**

### Explain uncommon abbreviations

Now some confusing variable names. Can you guess from [this block][stblock]?

```py
i = 0
st1, st2 = 0, 0
if compr_cigar[0].status != "=":
    st1 += compr_cigar[0].len1
    st2 += compr_cigar[0].len2
    i += 1
```

The arbitrary `i` is standard, and `len` = "length" is easy enough. But `st` 
isn't something I recognize. "State", "Saint", etc. don't make sense here.

At the top of the file is

```py
AlignedBlock = namedtuple("AlignedBlock", ["st1", "en1", "st2", "en2"])
```

Thus, I think probably `st` = "start" and `en` = "end". Or at least that's my 
best guess? In the excerpt I quoted, they seem to be finding the index of the
first non-`=` element, which is a kind of start.

But I had to cross-reference and make an assumption to figure that out. Would've
been nice if the name was spelled out. Maybe once where the `AlignedBlock` is 
set up, and once where it starts being used in the function I quoted from. Or 
at least use a longer, easier-to-guess abbreviation? I can figure `compr` = 
"compare" just fine because it's long enough to be distinguished.

### Code _can_ be self-documenting

Let's end on a positive note. The script [`visualize_cigar.py`][visualize] is 53
lines of clean, readable code. I can easily understand it with a single read.
Despite a lack of comments, the code is *self-documenting*.

Part of the reason is that it doesn't have the issues I brought up. The `-i`
option has a long-form of `--input`, for example. And the variable abbrivations
used are reasonable: `cx` and `cy` for coordinates within two strings, `x`, `y`
for arrays linked to `cx` and `cy` respectively, `cnt` for "count", etc. This is
very helpful. It means I can read the code *smoothly*. No brainpower is wasted
on figuring out what this or that means.

The legible names, and Python's basically-pseudocode syntax, are used to full
effect. For example, this loop:

```py
for len, mode in parsed_cigar:
	len = int(len)
	if mode == "M" or mode == "X" or mode == "=":
		cx += len
		cy += len
	elif mode == "I":
		cy += len
	elif mode == "D":
		cx += len
```

Okay, so we're looping through paired lengths and modes, and depending on the
exact mode, we add the length to one or both of the coordinate variables. Yay!
Quick and easy to understand. Even more so if (like me) you have some experience
with CIGAR strings and thus know what the symbols would mean. But the basic
structure is clear no matter what.

This is why self-documenting names are so important. With them, it's much easier
to create self-documenting code.

---

I read Japanese. Somewhat<sup>2</sup>. It takes a lot more effort than English,
and it's not that the structure is hard (though some rarer grammar trips me up),
or that I'm looking every other word up in the dictionary. The biggest issue is
that I have to look up many words *in my head*: I have to exert conscious effort
to figure out what individual parts of the sentence mean.

Similarly, in coding, it's a lot easier to smoothly read a passage if the 
individual bits are named well, because then they are automatic to understand, 
and all the brainpower can be devoted to parsing the overall structure.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

---

1. Sorry, Dr. Palmer <3 I know you thought I was headed your way.
2. Specifically, I read at a *Percy Jackson* level with use of a dictionary a
few times a chapter.

[argparse]: https://docs.python.org/3/library/argparse.html
[Code]: https://github.com/seryrzu/unialigner
[comparecigars]: https://github.com/seryrzu/unialigner/blob/main/tandem_aligner/py/compare_cigars.py
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1038/s41592-023-01970-4
[stblock]: https://github.com/seryrzu/unialigner/blob/c5a1eecab7bd17485a0fe3422684409c3e884f31/tandem_aligner/py/galign_blocks.py#L59-L64
[visualize]: https://github.com/seryrzu/unialigner/blob/main/tandem_aligner/py/visualize_cigar.py