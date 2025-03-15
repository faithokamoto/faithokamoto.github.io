---
layout: post
title: Don't Repeat Yourself
subtitle: herein I repeat standard advice
tags: [last-pass, process, style]
author: Faith Okamoto
---

A recent [pull request][PR] I made was *supposed* to just add a small function
to a larger codebase. But, while poking around the code, I ran into egregiously
non-[DRY][DRY] bits. Being who I am<sup>1</sup>, I refactored. Today's rant is
about DRY coding. I'm aware this has been done to death on the internet, but,
well, it's the first thing I thought to write.

## What is DRY code?

DRY stands for **D**on't **R**epeat **Y**ourself. Its antithesis WET<sup>2</sup> 
stands for **W**rite **E**verything **T**wice. Basically, have bespoke code
appear only once. Some examples, from the refactoring I just did:

* Two functions had the exact same set-up and clean-up with slightly different
inputs. I factored out the set-up/clean-up into separate helper functions (this
involved literally copy-pasting the code from one of the original functions) and
then simply **called the helpers from each function**. 
* Many snippets calculated the length represented by a struct by performing the
same set of bit operations. I factored out a helper `.length()` (copy-paste).
Then I used `.length()` **in place of all the identical bit operations**.
* Nucleotides were encoded as 4-bit numbers. (ACGT, but also a gap character and
the [ambiguous nucleotides][Nucs].) These numbers were simply copied wherever
needed, with no true central table. I created an enum `NucCode` to explicitly
**tie each nucleotide to its code**, and then used the `NucCode` enum wherever
nucleotide codes were used to check the underlying nucleotides.

## Why DRY?<sup>3</sup>

Hopefully my examples above had you nodding your head saying, yeah, that all
makes sense. Here are some benefits I've personally had from DRY code:

* I only have to change the logic in one place. If I'm improving logic, fixing a
bug, or just adding a new check, I only have to update one bit of code.
* I get less weird errors. When I have copy-pasted code, I'll *think* I updated
it everywhere, or I'll *think* that the code here works similar to the code
there, and then subsequently be very confused when those assumptions are proved
false. If I scan ten bitshifts throughout the file, my eye may skip over the
one different one. If have all those bitshifts instead call a central function,
everything is fine and dandy.
* My code becomes more readable. Instead of e.g.
    ```c++
    // Nucleotide length is stored as <complicated bespoke bit math>
    int length = <complicated bespoke bit operation>
    ```
    (which is admittedly better documented than the code I usually find), I get
    ```c++
    int length = curMut.length();
    ```
    The improvement should be obvious here. It's similar to the readability gain
    from factoring out helper functions: hide the logic elsewhere, just declare
    your goal and trust that it happens.
* I have a central thing to show others. For example, if I had to explain those
nucleotide codes, I much prefer passing over the enum instead of the hardcoded
conversion functions which I started with.

## How to DRY your code

So I've convinced you, or you were already convinced. Great. Here is the simple
method I used to DRY code:

1. Look at code. Think about code. What do you multiple times? Choose a thing.
2. Write a well-documented, well-named helper which does the thing.
3. Use your helper everywhere the thing is done.

Congrats! Your code is one bit DRY-er. Repeat until readable enough.

----

<sup>1</sup> what kind of person do you *think* would write a blog about coding
best practices?  
<sup>2</sup> hah hah aren't the coders funny  
<sup>3</sup> I couldn't resist (this is why I shouldn't allow myself to have
footnotes)

[DRY]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[PR]: https://github.com/TurakhiaLab/panman/pull/46
[Nucs]: https://www.dnabaser.com/articles/IUPAC%20ambiguity%20codes.html