---
layout: post
title: Automated tests
subtitle: Not just for individual functions!
tags: [testing]
author: Faith Okamoto
---

I've mentioned [testing][TestingTag] in [one prior blog post][ToyDataBlog], but
now I have a nice case study of developing automated tests. Also, it's sort of
my only thing I can write about? I was on a vacation for a week and a half,
y'all. In case you were wondering why the update is a little late.

(Did I actually get to the case study in this blog? No. Maybe next time.)

## Why do we need tests?

First off, if you're asking that, your code has bugs in it.<sup>1</sup> Testing,
especially [Test-driven development][TestDrivenDevelopment], is a way to
minimize bugs. Ideally you can take the bugs you know about (or at least think
to check for) all the way down to zero. The corollary of this is that *not*
testing is a great way to have bugs that you might've noticed at some point.

Good tests are completely automated. Once you're ready for code to be tested
(e.g. you finish a feature/script and want to add it to the main repository) the
test should trigger and check that you haven't broken anything which is supposed
to work. With a whole team collaborating to create tests, you're not reliant on 
just checking the bugs and edge cases that *you* would consider. Instead, you
get an easy way to check all the bugs that anyone thought might pop up.

I'm assuming you would like your code to have less bugs<sup>2</sup>

## What can you test?

Anything! Here are some [tests][vgTests] that [vg][vg] has:
* [command-line small graph conversions/viewing][ViewTest]
* [a lack of "yeet" in the code][YeetTest] (yes, [there were yeets][YeetCommit] for a brief time)
* [the `simplify()` function works as expected][AlignmentTest]
* [help-text matches underlying code for options][OptionTestingPR]<sup>3</sup>
* zip code trees (I'll let [Xian Chang's thesis][XianThesis] explain those) can
[handle a bunch of randomly-generated graphs][ZipCodeTreeTest]
* [a helper script runs without crashing][ScriptsTest]
* [the minimum supported compiler version actually is supported][CompileTest]

As you can see, these don't fit a single mold. Sometimes we call functions from
within the C++ code, and sometimes we run the tool on the command line.
Sometimes we decide to ban a word, and sometimes we force command line options
to be formatted correctly. Sometimes we use random data, sometimes we generate
specific data and expect a given result. Sometimes we even test things
peripheral to the code itself, such as a helper script or its compilation.

If you want your code to be able to do something, then you need to test it.

## How can you test?

Well, that's a whole post in itself. A post I'll probably write at some point,
but still, too much for now. Look up "unit test \<language\>" on your favorite
search engine. There are more ways than I know. In Python<sup>4</sup> I
favor the builtin library [unittest][unittestLib]. On GitHub you can set up
[automated workflows][GitHubTest]. Can't hurt to test it out, yeah?

---

1. I mean, *all* code more complicated than the intro stuff like "Hello World"
has bugs. But if you profess to have code that doesn't need tests, then the
chance of lacking bugs drops from "finding a unicorn" to negative.  
2. If you don't care, then, well, I'm honestly not sure why you're reading this
blog. Why care about style if you're fine with actual errors?  
3. Yes, I spent a week of my 1.5wk vacation hyper-focusing on a script for work.
Yes, this included weekends. Yes, "weekends" includes the day I went to my
friends' wedding. In my defense, I enjoyed it? The coding and the wedding, I
mean. Both. Yeah. That's my story and I'm sticking with it.  
4. Ah, Python. I miss you. Especially dealing with C++'s... quirks, I'll call
them quirks. More polite than what I would normally say.

[AlignmentTest]: https://github.com/vgteam/vg/blob/379c37db5d3f0f7f1a084782ce72dfcad1d6f60d/src/unittest/alignment.cpp#L19
[CompileTest]:  https://github.com/vgteam/vg/pull/4653
[GitHubTest]: https://docs.github.com/en/actions/how-tos/writing-workflows/building-and-testing
[OptionTestingPR]: https://github.com/vgteam/vg/pull/4654
[ScriptsTest]: https://github.com/vgteam/vg/blob/master/test/t/99_scripts.t
[TestDrivenDevelopment]: https://en.wikipedia.org/wiki/Test-driven_development
[TestingTag]: https://faithokamoto.github.io/tags/#testing
[ToyDataBlog]: https://faithokamoto.github.io/2025-03-02-the-art-of-toy-data/
[unittestLib]: https://docs.python.org/3/library/unittest.html
[ViewTest]: https://github.com/vgteam/vg/blob/master/test/t/03_vg_view.t
[vg]: https://github.com/vgteam/vg
[vgTests]: https://github.com/vgteam/vg/tree/master/test/t
[XianThesis]: https://escholarship.org/uc/item/9wk1v3np
[YeetCommit]: https://github.com/vgteam/vg/commit/36d47dfb3872a16c554b5eed828a642a804871d4
[YeetTest]: https://github.com/vgteam/vg/blob/master/test/t/100_code_quality.t
[ZipCodeTreeTest]: https://github.com/vgteam/vg/blob/379c37db5d3f0f7f1a084782ce72dfcad1d6f60d/src/unittest/zip_code_tree.cpp#L3336