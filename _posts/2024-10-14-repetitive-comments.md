---
layout: post
title: Repetitive comments
subtitle: Comments that repeat the code (;D)
tags: [comments]
author: Faith Okamoto
---

I've been using [ChatGPT][ChatGPT] to write code for a class. (This is
explicitly encouraged by the professor.) Its default style has one of my pet
peeves: comments that do nothing but repeat the code. The LLM does this because,
its training data, lots and lots of humans wrote these kinds of comments.
Thus, I'll explain to my fellow humans why they should stop.

## Defining a repetitive comment

If a comment adds *literally no new information* to a surface-level read of the
code, it's repetitive. This comes in two flavors:

- Reading the code in English (or another natural language)  
    ```
    # Do something if the current interval overlaps the test interval
    if current_interval.overlaps(test_interval):
        do_something()
    ```

    ```
    # Read lines from file
    fasta_file = file.readlines()
    ```
- Stating an obvious consequence
    ```
    if cur_line.has_end_char():
        # Stop early
        break
    ```

    ```
    # Speed up
    speed += 1
    ```

The boundary between the flavors, and the boundary between repetitive and useful
comments, is up for debate. Still, many comments clearly fall into "uselessly
repetitive". How does "Read lines from file" add to `file.readlines()`?

## But aren't comments useful?

Yes, comments that *provide useful information* are wonderful!

But short repetitive comments get in the way. They are distracting. A reader
sees the comment, thinks it's relevant, and then wastes time. Worse, now you,
the developer, have to maintain both the code and the repetitive comment. If
the code changes, the comment becomes confusing. It describes nonexistent code.

Comments are for useful insights. Using them sparingly means each is more likely
to be read and seen as important. Cluttering up the screen with repetitive
comments means it's more likely people will skip the ones that matter.

## What comments should I use, then?

As I said: comments which actually serve a purpose. This can even include simple
summary *of a section of code*. For example, the following are useful comments:

```
# Read command-line arguments into variables
bed_file1 = sys.argv[1]
bed_file2 = sys.argv[2]
fai_file = sys.argv[3]
# Default number of permutations is 10,000
n_perms = 10000 if len(sys.argv) == 4 else int(sys.argv[4])
```

The first comment serves as a summary of the block. By using comments such as
these sparsely, a reader may scan the code and take in its general structure.
This helps them focus on whatever part matters most to them.

The second comment provides useful information. Why is `n_perms` being set to
10,000? Because that is the default. By contrast, a comment saying, "Use 10,000
permutations if no argument is given" would be repetitive, since that's exactly
what the line does. Adding the note about the default, however, is useful.

That's it. If the code makes as much sense without the comment as with it, then
the comment is useless repetitive clutter. If the comment adds something, even
if that something is just a section summary (e.g. a docstring), it's useful.

[ChatGPT]: https://chatgpt.com/