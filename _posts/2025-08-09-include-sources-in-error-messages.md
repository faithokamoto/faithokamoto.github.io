---
layout: post
title: Include sources in error messages
subtitle: So what failed, exactly?
tags: [errors]
author: Faith Okamoto
---

I've mentioned before that [error messages should be useful][UsefulErrorsBlog].
Today I'll discuss a specific facet of usefulness that can easily be overlooked:
having error messages say where they come from.

## Where error messages are from

You might say the source of the error is obvious. It's the code, right? 
Somewhere in the code you just ran.

Yeah, not so much. Once you get past very simple scripts, the possible locations
for an error explode. One file might call a function from another file, which
calls a function from a file buried in a subfolder, which calls a function from
a dependency, and all your poor user knows is they tried to run a single
terminal command.

Plus, it's not guaranteed that the error message actually appears verbatim
anywhere in the code. Yes, control-F/`grep` will sometimes work, if you know
which files to search. But not always. If the error message is built up in
multiple locations, or if parts of it are dynamically generated based on the
specifics of what failed, then you'll be out of luck. 

Especially if your program exited gracefully instead of just crashing. Say what 
you will about how ugly stacktraces are. At least they tend to tell you the line 
number that caused the problem.

## How to attach sources

Any sort of standardized format will do. For example, taken from `vg` again
because guess who pays my stipend, look at [this function][IndexRegistry]:

```c++
void copy_file(const string& from_fp, const string& to_fp) {
    ifstream from_file(from_fp, std::ios::binary);
    ofstream to_file(to_fp, std::ios::binary);
    if (!from_file) {
        cerr << "error:[IndexRegistry] Couldn't open input file " << from_fp << endl;
        exit(1);
    }
    if (!to_file) {
        cerr << "error:[IndexRegistry] Couldn't open output file " << to_fp << endl;
        exit(1);
    }
    to_file << from_file.rdbuf();
}
```

Here the `[IndexRegistry]` indicates where the error originated from. This is
actually pretty important here, since this isn't a file that the user will be
directly calling. Its algorithms are used by various subcommands. Thus, if I run 
e.g. `vg cluster` and get this error, I'll know who to blame.

If you look through `vg`, you'll see that quite a lot of places use a similar
format for error sources.<sup>1</sup>

## How specific to be

Even narrowing down to a specific file as the source of the error is incredibly
useful. Narrowing down further has trade-offs. Namely that now your error might
get too unwieldy. I won't stop you, though.

As a general rule, the source included just needs to be:
1. Accurate<sup>2</sup>
2. File-specific (so that the debugger can focus on one file in detail)
3. Descriptive (to be clear which file is being talked about)

With that information, whomever is trying to debug their error should be able to
easily find where it came from. Which, honestly, is usually half the battle.

----

1. Is the order of "error", the source in brackets, and the colon inconsistent? 
Yep. Are sources included in all warnings? No. Guess what my current side
project is :D
2. You may think this is a joke, but it is not. Copy-paste jobs go wrong all the 
time, which is why `vg augment` may [error][Augment] claiming to be `vg call`.


[Augment]: https://github.com/vgteam/vg/blob/07940956a27a8ac38254d7f993373e458c301ec4/src/subcommand/augment_main.cpp#L233
[IndexRegistry]: https://github.com/vgteam/vg/blob/07940956a27a8ac38254d7f993373e458c301ec4/src/index_registry.cpp#L130
[UsefulErrorsBlog]: https://faithokamoto.github.io/2025-01-10-useful-error-messages/