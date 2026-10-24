---
layout: post
title: Skip steps at your peril
subtitle: for I will send my minions
tags: [tutorials]
author: Faith Okamoto
---

I recently had to run an analysis which I had never done before. I therefore
asked my labmates for help, as I knew some of them had been testing this. I was
provided with help. In the end, I got to my goal, but with more pain than was
necessary. Now I'm going to complain about it.

## What was missing

I was given a list of steps with copy-pastable commands. *Great!* I thought.
*This should be a piece of cake.* (Narrator: it was not a piece of cake.)

- Several filenames were given without indicating the directory in which to find 
the file. I had to go digging around to figure out the correct path.
- Two steps required the use of an external tool. Neither of these tools were
immediately accessible in the environment I had. Or, one of them _was_, but with
the wrong version.
- At one point I had to perform a filtration step which was not warned about in
advance. Or documented anywhere. I only found out about it since I was getting
weird errors, and luckily a person who knew what was happening saw my message.
- Some steps were given in English that I did not know exactly how to carry out,
e.g. "sort and index the file". Uh. How? I hadn't done that before. Those turned 
out to require stringing together a few commands in what is likely a standard 
method but which I had to figure out by myself.

## "Obvious" steps

The key issue here is that, to the person writing out these instructions, the
bits I stumbled over were too obvious to merit mentioning. They know where their
files are. They already have all the necessary dependencies set up. They know
all the details of each step, to the point that they don't see a need to explain
how to index that file. These problems are _invisible_ to an expert, yet very
annoying to a newbie.

It's hard to notice these when you're the expert. I'd know, given that I've
fallen into similar holes in the past. It is, however, worth it to try. Not only
in the sense of "worth it" where it gives you fuzzy butterflies for being a good
community member, but also in the sense where if the instructions you make are
easy to follow then people may bug you less about clarifications.

## Avoiding skipping

Like any piece of writing, there are edits you can do by yourself, and there is
feedback that only other people can give you. First, it behooves you to go
slowly through all the instructions. Ask if an idiot could follow your steps. If
the answer is no, ask if you care about this kind of idiocy. (There are things 
that can be safely skipped, e.g. how to select a checkbox.) If reasonable, edit 
for clarity.

Then hand the instructions off to someone else. Ideally someone unfamiliar with
the issue at hand, in order to imitate the kind of person you're trying to help.
Whatever they struggle with, try to fix. Repeat as desired. Though, practically,
probably repeating isn't going to happen, and that's OK. Also, if you get
feedback later from users, then incorporate that too.

Voila. A (hopefully) idiotproof tutorial.