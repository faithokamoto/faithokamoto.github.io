---
layout: post
title: Knowing what to leave out
subtitle: this is one of my positive ones
tags: [published-code-critique, gitignore]
author: Faith Okamoto
---

I spend a while complaining about what people should add to their code.
(Comments. You should add [comments][CommentsTag]. Also a [README][ReadmeTag].
Also [documentation][DocumentationTag]. Also... but I repeat myself.) I thought
it might be interesting to look at what people should leave out. And since this
is a topic that benefits from specifics, I'm using it for a critique.

This month's paper: Andrukhovskyi, D *et al.* Efficient Algorithms for Pangenome
Personalization. *26th International Conference on Algorithms for Bioinformatics*
2026. doi: [10.4230/LIPIcs.WABI.2026.8][DOI]

## Original code

This tool is on [GitHub][Code]. I'm focusing specifically on their 
[`.gitignore`][DotGitignore].

## Critique

Remember that "critique" has a neutral meaning which can also involve praise :)

### What's a `.gitignore`?

For this post to make any sense, you have to know what a `.gitignore` file is,
and for that to make any sense, you have to know what `git` is. So: `git` is a
version control system. Very basically, it's a way to track changes in files
over time. Like the history function in Google Docs, except for all the files in
a folder.

And `.gitignore` is a way to tell `git` which files to not track. This one is:

```
*~
.snakemake
or-tools*
include/
```

### Good things to ignore

The items here are a nice, simple list of examples of things you should put in
a `.gitignore`. Let's go through them:

- `*~`: ignoring a specified affix (prefix or suffix). Sometimes you know that
there will be files that the user will need, but that will be too big or
whatever and thus would be difficult to track. Temporary files, for example. If
you know that all your temp files have a prefix `temp`, then you could ignore
`temp*` and voila they won't pollute your `git` history.
- `.snakemake`: environment/log files. While it's important to specify what
environment should be used to reproduce a computation, there are much, much
better ways to do so than literally dumping the exact fiddly bits used. These
tend to involve a bunch of small, complex, boring files that are always being
messed with by processes that we don't care about so long as they work.
- `or-tools*` & `include/`: dependencies. As long as you've included details
about which dependencies to use and how, your dependencies should be
reproducible. Dumping the exact installations from your own setup would a) take
up a bunch of space, b) involve a bunch of files that aren't really yours, and
c) probably not work on any other computer, due to how things install.

Anyhow, I thought this was nice :D Ignore temp files, output files, log files,
environment stuff, etc. You want to track the underlying code that you control.
And just that.

----

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[Code]: https://github.com/fmfi-compbio/2paths
[CommentsTag]: https://faithokamoto.github.io/tags/#comments
[CV]: https://faithokamoto.github.io/cv/
[DocumentationTag]: https://faithokamoto.github.io/tags/#documentation
[DOI]: https://doi.org/10.4230/LIPIcs.WABI.2026.8
[DotGitignore]: https://github.com/fmfi-compbio/2paths/blob/main/.gitignore
[ReadmeTag]: https://faithokamoto.github.io/tags/#readmee