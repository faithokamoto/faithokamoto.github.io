---
layout: post
title: Give me a roadmap
subtitle: or, how *not* to onboard a newbie
tags: [starting-projects, documentation]
author: Faith Okamoto
---

You know how I go on about the importance of [documentation][DocumentationTag]?
It's because I want to avoid being the cause of pain like I experienced just
yesterday. Let's run back the tape.

----

## My goal

I want to update one of our algorithms. A colleague identified a function which
seems likely to do exactly what we want. It requires passing in an object of a
certain class. Then it performs some magic and spits out my lovely answers.

Okay, great! So now what I need to do is construct one of those objects. I 
located the files where the relevant class is defined and implemented. Time to 
read up on how this thing works.

What could possibly go wrong?

## What went wrong

Well, here's the thing. You can't read no documentation if there's no
documentation to read.

I pulled up to the class definition and was greeted with, I am not joking, this
comment. This was all I saw above the class definition.

```c++
// TODO: the metadata could be removed and only added to the protobuf at serialization time
```

Great. Wonderful. Um. What?

Within the class itself, I found a long list of functions with absolutely zero
comments, then another list labeled `// annotation interface` with another TODO
(nothing in sight about what annotations are, though), then a list of member
variables. And, folks, that was the entire contents of the class.

[It did turn out that the member variables were described somewhere else, but
seeing as that somewhere else was in a different repository entirely and not
clearly linked from the class itself, I'm not giving it any points.]

## What did I want?

As someone entirely new to this class, what I wanted was a high-level _roadmap_.
This is a concept that goes by plenty of names. And no, I don't just mean a
class [docstring][DocstringsTag] with a two-line description. I mean something
that a new person can use to get orientated.

What might a roadmap have?

- High-level description of what the class represents, and how each member
variable fits in to that.

- How and why the user is expected to instantiate, modify, and otherwise use
objects from this class.

- Where this class is currently used (i.e. where I can go to find an example).

From that, I would be able to get my bearings. For example, I knew I wanted to
create an object with a certain structure. If I knew what the fiddly bits of the
class represented, and which functions I'm expected to call to fiddle with them,
then I'd be able to set up the object I need.

Do I need annotations? What _are_ annotations? Which variables am I supposed to
set myself, and which will be done by the magic function once I've prepped my
object? Why would I use one similarly-named function over a different one? What
general pattern should I use to add information into a blank object? All
questions I had which this code did not answer.

Instead I had to resort to searching through the codebase for where this class
had been used (frustratingly, often without explanatory comments) and then
reverse-engineer how I was supposed to work with it. So much work that could
have been bypassed if I just had a map.


[DocstringsTag]: https://faithokamoto.github.io/tags/#docstrings
[DocumentationTag]: https://faithokamoto.github.io/tags/#documentation