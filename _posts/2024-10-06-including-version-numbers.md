---
layout: post
title: Including version numbers in your code
subtitle: What do I need to run this thing?
tags: [imports, software]
author: Faith Okamoto
---

You should always specify the versions of any code dependencies. Perhaps not so
far as the exact Windows operating system. But, using package versions `1.1.0`
or `1.2.1` can and does affect the code.

## Where do version numbers go?

Version numbers can be documented in multiple places. What matters is that this
information is somewhere. Plus, that "somewhere" should be simple to find. These
versions represent what you developed with. Be absolutely sure this specific
environment works with your code. Ideas for how to include version numbers:

- A table in the [README][README] with all dependencies and version numbers.
- A separate file (e.g. CSV, [conda `.yml`][Conda]) specifying the environment.
- If output is included (e.g. [Juypter notebook][Juypter], [R Markdown][RMark]),
print the version numbers.
- In the [script docstring][ScriptDocstrings].
- Next to the first use of each dependency (e.g. the import statement).

## Why do other people need to know my version numbers?

If you want other people to use your code, you must tell them how. If you use a
feature implemented in version `4.3.0`, tell them. If you use version 1 of a
tool because version 2 changed the input format, tell them.

Try to minimize the setup time of an end-user wants to run your code. For this
reason [conda environment files][Conda] are quiet useful. They are a one-stop
shop to set up all necessary dependencies.

This applies even if you're not aware of any version issues. Later breaking
versions may be released, or there might be subtle issues from a combination of
a special case and a different version number. Always specify. This removes one
of the major headaches when starting with new code.

## Why do I need to know my version numbers?

Maybe you buy my argument for including version numbers in publicly released
code. Why do you need them for private code?

Well, do you plan to ever update the software you have installed? If you're not
going to keep using the same Python version as when you started programming,
then notating the current version number along any private code is still useful.
Then, if you want to use the code later but it has mysterious errors, you can at
least rule out the differing version numbers as the cause.

Plus, you never know when you might want to release some private code. If you
ever do so, already having the version numbers written down will be a relief.

[Conda]: https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#sharing-an-environment
[Jupyter]: https://jupyter.org/
[README]: https://www.makeareadme.com/
[RMark]: https://rmarkdown.rstudio.com/
[ScriptDocstrings]: https://faithokamoto.github.io/2024-09-24-script-docstrings/