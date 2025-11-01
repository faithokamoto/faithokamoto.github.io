---
layout: post
title: The joy of tidying code
subtitle: a fulfilling side project
tags: [motivation, refactoring]
author: Faith Okamoto
---

I recently got a [massive side project][CheckFilesPR] (that I'd previously
[hinted][ErrorSourceBlog] about) merged in to the master branch. A good time to
reflect on why I even bothered.

----

## Finding a reason

It's not like improving the appearance of error messages can be counted as part
of my thesis. Time in grad school is limited. Why do I put effort into tidying
this code base?

Improving usability is, far too often, nobody's job. Scientists have a rather
bad habit of making code that works _for us_, writing a paper, releasing a link
into the wild, and then... moving on to the next project. Publish or perish, eh?
Releasing an update that improves progress logging won't get you anything new to
be cited; releasing a new flimsy tool just might. But then it becomes difficult
to stand on the shoulders of giants and all that jazz.

The external incentives to clean up academic code simply don't really exist. So
you need to find other reasons.

## Practicalities

If I need to explain myself to someone, there are ways I do so. For example:

* I, and other people I work with, are constantly using these tools; improving
their usability makes our jobs easier. The less that someone has to ask the
developers to explain an error, the more time both of us have to do our work.
* Having a low-brainpower side project gives me something to "relax" with. If my
actual work is stuck or waiting for whatever reason, I can turn to my side
project and still get something done.
* Chipping away at the perception of our tool being user-unfriendly might mean
more people use it, which might mean we get more citations down the line.

But are any of those my real reason? Nah. My real reason is, as the blog post's
title suggests...

## Joy

I _enjoy_ my side projects. Working on them brings me calm, a sense of being
useful, constant bite-sized accomplishments. Fixing small issues is relaxing.
There's a reason I do a lot of volunteer copy-editing for an Internet community
that I'm fond of, and the reason is very simple: I like copy-editing. Code
cleanup is similar.

The best reward is, of course, when I see my side projects jump into action. My
[new unit tests][UnitTestBlog] have already prevented a few errors from being
introduced. These are the fruits of my labor of love. My labor of joy.

But if you're not the kind of person who finds joy in this stuff, then maybe you
can just re-read the previous section.

[CheckFilesPR]: https://github.com/vgteam/vg/pull/4689
[ErrorSourceBlog]: https://faithokamoto.github.io/2025-08-09-include-sources-in-error-messages/
[UnitTestBlog]: https://faithokamoto.github.io/2025-08-02-developing-a-testing-script/