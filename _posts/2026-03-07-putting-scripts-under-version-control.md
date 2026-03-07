---
layout: post
title: Putting scripts under version control
subtitle: Surprisingly nice
tags: [file-level, version-control]
author: Faith Okamoto
---

My brain is absolute mush after this week's PhD recruitment events, so it's not
a great time for writing a blog post, but at least I do have a topic. My
current priority is helping to get a paper out. As that project circles towards
completion, I've put the code under version control. I now believe that this is
a good thing to add in general to my [file organization][OrganizingBlog].

## Practical set-up

I don't want to figure out how to set up just local version control. I know it
can be done. But I am not a software developer (okay I am, sort of); I'm a
bioinformatician. So I just made a [repository][GitHub] on GitHub and then 
cloned it to my computer cluster. GitHub knows how to set up a git thingy.

I copied in some of the files that I was already using, set up a README, etc.
One big important thing was making a [`.gitignore` file][gitignore]. I have
logfiles and inputs that I either can't (because unpublished data) or don't
want to (because too big etc.) put under version control. So git ignores them!

Now I have an initial state that I can simply chip away at with small edits.

## Benefits

Most of the time when I edit a script, I'm only editing a small part. There was
a bug in this option. That file moved locations. I need to temporarily get rid
of a few sections. etc. With version control, I'm able to easily track which
changes were made when and why. I can charge on ahead with tweaks without worry
over if I need to remember a previous state. Git remembers it for me!

Also, now I have a GitHub for this project. That makes it easier to share with
other people. I can use the web interface for links and even to track history
of specific files. Quite nice.

----

I'll probably be setting up version control for any nontrivial script 
collections I make in the future.

[GitHub]: https://github.com/faithokamoto/centromere-haplotype-sampling-pipeline/
[gitignore]: https://github.com/faithokamoto/centromere-haplotype-sampling-pipeline/blob/main/.gitignore
[OrganizingBlog]: https://faithokamoto.github.io/2024-11-16-organizing-files/