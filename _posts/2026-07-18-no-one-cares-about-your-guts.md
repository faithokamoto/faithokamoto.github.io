---
layout: post
title: No one cares about your guts
subtitle: give the people what they want
tags: [documentation, functional-programming]
author: Faith Okamoto
---

I had the particular experience of listening to someone else's code review in a
meeting this week. A fellow PhD student talked to the senior dev about a
proposed change.<sup>1</sup> One point was interesting enough to write about.

## What is a function for, anyways?

I've tagged this with ["functional programming"][FunctionalProgramming]
because that's the paradigm I want to talk about. Functional programming means
that your program is a cascade of individual function calls.<sup>2</sup> A 
_function_ is a self-contained bit of code that does a thing. It might modify 
an input, toggle a global state, perform a search, etc.  A function will ideally 
[do one thing][OneThing], and do it well.

What's the point of hiding code in functions? Well, because of that hiding. If I 
have a function to `sort_array()`, I don't have to worry about how that sorting 
happens. All I have to do is plug it in. It's a lot easier to just trust the
function to do its job. No mucking in the weeds needed.

## Documenting a function

If the point of functions is to drop in a discrete bit of functionality, then
the important part of documenting it will be to define that functionality.

- What **inputs**? If you pass two strings, a `query` and a `reference`, what do
each of those mean? What do I need to make sure of before passing my input?
- What **outputs**? Does `sort_array()` return the fully sorted array, or a
True/False value indicating whether any elements were moved, or nothing at all?
What guarantees can I rely on from the outputs?
- What **errors**? In what cases does this function fail, and what happens when
it does? Is passing a negative number problematic, or a graph containing cycles?
I realize it's not possible to anticipate all edge cases, but at least make a go
of it for any you know of in advance.
- What **effects**? If something happens that escapes the function's interior,
what is it and why?

And I think that last one is often the problem.

By "effects", I most assuredly do not mean "internal workings". That is, I do
not mean by what method the function's job is _effected_. I mean what a user
should expect to happen _outside_ the function. For example, a function could
delete a file on the user's machine. That's external to the function itself.

## No one cares about your guts

Inside the function (its implementation) doesn't matter for documentation. The
implementation can change whenever. As long as the function's interface stays
constant, the user doesn't need to care.

My fellow student was documenting the details of _how_ their functions went 
about each assigned job. That's not what function docstrings are for. If I'm 
reading a function docstring, I want to know just what the function does. Not 
how it does what it does.

Yes, I realize that as someone who develops algorithms, caring about how things
work is my job. But I only care how things work when I'm trying to _understand_
them<sup>3</sup>: debug them, modify them, copy them. Most of the time I just
want to use them. In which case I want a brief function docstring sans guts.

----

Note that "no one cares about your guts" is a general principle that applies to
anything people are meant to _use_ without necessarily understanding. Do you
care how your operating system works? Or your code's compiler? Or that command
line tool you downloaded out of desperation because this paper needs one more
analysis by tomorrow? Probably not. You just want to get them to work.

----

1. This is purposely vague such that it won't be searchable later. Probably if
you went digging right now you could figure out who I'm talking about, but that
would require someone to be reading my blog. I mean, besides the scrapers. In
any case the point of the post is not to name-and-shame, so no name is named.
2. Wow, wonderful definition you got there, Faith. 
3. In this case, I turn to the function's internal comments and/or an external
algorithm writeup, not the function docstring.

[FunctionalProgramming]: https://en.wikipedia.org/wiki/Functional_programming
[OneThing]: https://softwareengineering.stackexchange.com/questions/402979/what-does-it-mean-for-a-method-or-a-function-to-do-one-thing