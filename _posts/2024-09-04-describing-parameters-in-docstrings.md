---
layout: post
title: Describing parameters in docstrings
subtitle: (please do)
tags: [parameters, docstrings]
author: Faith Okamoto
---

Let's dive into how and why [docstrings][PEP257] should describe parameters.

## What's a docstring?

As [PEP 257][PEP257] says,

> A docstring is a string literal that occurs as the first statement in a
module, function, class, or method definition. Such a docstring becomes the
`__doc__` special attribute of that object.

Similar constructs exist in other languages. The main idea is that important
units of code, e.g. functions, should have in-code documentation. For example,
this is a single line docstring:

```python
def inverse_reciprocal(x: float) -> float:
    """Compute the inverse reciprocal of x."""
    return -1.0 / x
```

And this is a multi-line docstring:

```python
def calculate_total_bill(n_brownies: int, n_cookies: int) -> int:
    """Calculate the total price of a bake-sale order.

    Brownies are $2 and cookies are $1.
    For interpretability, only pass positive integers.

    Parameters
    ----------
    n_brownies: int
        Number of brownies purchased on bill.
    n_cookies: int
        Number of cookies purchased on bill.
    
    Returns
    -------
    total: int
        Total price of order.
    """
    return 2 * n_brownies + n_cookies
```

There are many docstrings styles. Herein, I use the [Numpy][NumpyDocstrings]
format, but any format with all necessary information is fine.

## What's a parameter description?

A parameter description is exactly what it sounds like: a description of a
parameter. This includes, when applicable and not immediately obvious:

- **name** (e.g. `chrom`)
- **type** (e.g. `str`)
- **default value**, if applicable (e.g. `None`)
- **what it means/represents** (e.g. `chromosome to analyze`)
- **what it does** (e.g. `only SNPs on this chromosome will be used`)

(For an example of "immediately obvious", see `inverse_reciprocal` above.
Another line describing `x` would be repetitive.)

If not obvious, you **must include descriptions of your parameters**. Please.
I've had the displeasure of using code with unclearly documented parameters. 
It's... not pleasant.

## Why are parameter descriptions needed?

I'll illustrate why such descriptions are essential by an example from the
aforementioned struggle. I was alpha testing, trying to use some code without
much handholding by the original author. Thus, I relied on the documentation.

I determined that I needed a particular function, but wasn't sure what to use
for its parameters. Two had similar names: `window` and `ldwin`. I presumed the
latter was an abbreviation for "[LD][LD] window". However, the docstring only
had parameter names, types, and default values. That is, it was simply repeating
the type hints.

Some questions I had which would have been answered by a parameter description:

- How are `window` and `ldwin` different?
- What units are `window` and `ldwin` in? (e.g. SNPs/variants, base pairs, kbp)
- Is this the full window size (from end to end) or half (from center to end)?
- What is each window used for? Is some analysis run within the window? Is the
window used for removal of variants (for `ldwin`, due to high LD, maybe)?
- Is the window static or does it shift?
- How were these default values chosen? If I were to change them, what effect
would that have?

I spent a long while digging up answers from the function's code itself. 

Treat public-facing functions as an [API][API]. (I mean, they are. I think?)
Users shouldn't have to look into its interior to figure out how to use it. They
should be able to read a tidy description, understand their options, and then
confidently pull a few levers to perform a desired action.

I'm sure the original author of that code knew the difference between `window`
and `ldwin`, what each represented, and when each should be changed. But I sure
didn't. Never assume your users know what you're thinking. Think of the
documentation you would want to read, then write it.

[API]: https://www.howtogeek.com/343877/what-is-an-api/
[LD]: https://link.springer.com/chapter/10.1007/978-3-030-61646-5_2
[NumpyDocstrings]: https://numpydoc.readthedocs.io/en/latest/format.html
[PEP257]: https://peps.python.org/pep-0257/