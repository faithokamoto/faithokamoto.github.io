---
layout: post
title: Using keyword arguments
subtitle: Even when you don't have to
tags: [parameters, naming]
author: Faith Okamoto
---

You probably use [functions][Functions]. (If you don't use functions, then, um,
please do.) Those functions probably have parameters. When you call a function,
you pass specific values to those parameters. Today's post is about using
keyword arguments during those invocations.

## What's a keyword argument?

This concept has multiple names. In Python it's "[keyword arguments][Kwargs]",
in R I honestly have no idea but it uses [three dots][Dots] so I call them "dot
args". In general, it means that instead of calling some function as:

```
cluster(cleaned_matrix, 5, 1000, 42)
```

You would instead use:

```
cluster(data=cleaned_matrix, k=5, iterations=1000, random_seed=42)
```

That is, instead of relying solely on argument order to indicate which parameter
is doing what, the function call itself includes the names of each parameter. In
this case, apparently `cleaned_matrix`'s data will made into 5 clusters, with
1000 iterations and a random seed of 42.

## Why bother?

For readability and the sake of others, including you a month later, who have to
figure out what in the world that call to `cluster()` is doing. (Yes, I sound
like a broken record.) The reader does not want to stop and search for what the
third argument of this function does. The reader does not want to debug an issue
which comes from having only eight of the nine necessary arguments. The reader
just wants to know: what is the function doing, right here, right now?

Also, humans simply cannot hold long lists in working memory. "If you have a 
procedure with ten parameters, you probably missed some." ([source][Epigrams],
Alan J. Perlis) - long lists of unclarified arguments are just *asking* for
trouble. Including clarifying names makes for simple reading.

Sometimes you have the option of whether to use an argument name or not. For
example, the pandas `DataFrame.min()` has [three default parameters][Min], of 
which none *need* to be named. However, who's going to remember which of the two 
booleans (`skipna` and `numeric_only`) comes first? If your answer is "me", then 
congrats, but you're not the only person reading your code. Just a few names
will clarify what `min(1, True, True)` does.

On that note, what *does* `min(1, True, True)` do? Are you sure I didn't swap
those boolean argument names to trick you?

Use keyword arguments. Even when you don't have to. Please.


[Dots]: https://cran.r-project.org/web/packages/wrapr/vignettes/Named_Arguments.html
[Epigrams]: https://www.cs.yale.edu/homes/perlis-alan/quotes.html
[Functions]: https://www.geeksforgeeks.org/functions-programming/
[Kwargs]: https://docs.python.org/3/tutorial/controlflow.html#keyword-arguments
[Min]: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.min.html#pandas.DataFrame.min