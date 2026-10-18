---
layout: post
title: Yes, code quality matters
subtitle: it really, really does
tags: [readability, llm, rant]
author: Faith Okamoto
---

I went to a seminar talk recently about the impact of LLM usage in CS education.
When chatting with folks afterwards, a prof<sup>1</sup> expressed an opinion
with which I _strongly_ disagree. Paraphrased from memory:

> In the future no one will care about code's quality so long as it works.

## The argument, in more detail

An analogy was drawn with the assembly code of yore. In ye olden days, there
was no option but for programming to be at this very lowest level of individual
instructions to the processor. Then we transitioned to higher-level languages
such as C++ or Python. These let us write code which is shorter and more
readable.<sup>2</sup> Compilers/interpreters eventually translate everything
into assembly code, yet very few people will ever care how this process works.

The prof's argument was that source code, the C++/Python, will go the way of 
assembly code. Everyone would work at the LLM prompt level instead and not care
about reading what's generated. Doesn't matter if it's impossible for a human to 
parse, because humans will rely on LLMs for all interactions with the codebase.

## LLMs are not gods<sup>3</sup>

One of the premises here is that LLM poking will always be good enough. When you
tell it to do a thing, it will do the thing, or if it doesn't then you'll notice 
and tell it to fix the thing etc. This runs directly anathema to the standard 
advice to carefully vet LLM generated code.<sup>4</sup> Placing unquestioning 
faith in LLM code means treating it like a god, and that is right out for me.

Yes, I do not check the assembly code that my C++ compiler generates. I've never
even taken a class in assembly<sup>5</sup>. But the C++ code I write is still
_deterministic_. It carries around all its context within itself, is externally
documented, and will do exactly what it says it does. On the other hand, LLM
chat logs tend to be specific to the user. Plus they can very confidently tell
you that they've done something which they haven't done.

In short: yes, you have to read the code which is generated to be confident that
it is correct.

----

Also, if you want to show your code off to someone else, you probably want that
other person to understand what's happening without resorting to LLM, yeah?

----

1. Whom I will not name both because I don't name-and-shame, and because I
genuinely have no idea what their name is.
2. Python more than C++, but both are better than assembly.
3. For the curious, I do believe in a God.
4. This advice is often presented as a defense of LLMs, as in complains are met
with reassurances that all they need to do is vet more carefully.
5. Thankfully, in the great fight between the UCSD biology and CS departments on
classes required for bioinformatics majors, assembly didn't make the cut.