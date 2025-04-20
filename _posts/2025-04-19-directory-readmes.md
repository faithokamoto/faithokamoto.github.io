---
layout: post
title: Directory READMEs
subtitle: From the list of "things I wish other people did"
tags: [file-level, documentation, readme]
author: Faith Okamoto
---

I've mentioned that I [make a README as the first file][Process] in any new
project directory. Here, I'll detail what goes in this README.

----

1. **Header**: a one-sentence summary, followed by contact information

    I expect someone new to go to the [README][README]. Starting with the
    directory's purpose lets them decide how interested they are. Then, if they
    have questions, or just want me to clear up space, they can contact me.

    If this project has associated documents, such as a [notebook][Notebook],
    a slide deck, etc., then I link those as well for quick reference.

2. **Introduction**: a paragraph or so the motivation for this project.

    To be honest, this is mostly for myself. Keeping a short reference for the
    thrust of the project keeps me on track. Plus, if anyone asks, I have this
    nice little intro pre-written.

    Also to be honest, this part README often gets skimped on until later, when
    I'm more sure what I'm doing.

3. **Order of operations**: exactly what analyses I ran, and in what order.

    This directory presumably has files. Other people will presumably be
    interested in how those files got there. Thus, I explain which scripts were
    run, in which order, with which inputs, etc. Sometimes perfect reproduction
    isn't possible. For example, I may be actively developing a script/workflow,
    but still have files produced from a previous version. I still record what I
    did, including that it was a previous version.

    This section is also very useful for me. I try to update it often. No more 
    forgetting how to re-create that one file; I have it right here!

4. **Dependencies**: a list of tools/packages/etc. along with version numbers.

    [Version numbers][VersionNums] are great. This section is especially useful
    when I come back to a project, since I might've updated my tool versions in
    the interim. I can check exactly what I was using in ye olden days of, say,
    a year ago. Ideally I even set up a conda environment for myself. (The
    command to create the environment would be in this section.)

----

Those are the basic sections. I'll sometimes have more detail. Sometimes less,
though usually that's just at the very start of a project. I try to update this
every so often. For example, when I send off a big job, I'll go back to the
README and record what I've done up to that point.

I find keeping a directory/project README to be useful to myself and others.

[Notebook]: https://faithokamoto.github.io/2024-11-23-dry-lab-notebook/
[Process]: https://faithokamoto.github.io/2024-11-16-organizing-files/
[README]: https://www.makeareadme.com/
[VersionNums]: https://faithokamoto.github.io/2024-10-06-including-version-numbers/