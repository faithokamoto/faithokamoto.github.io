---
layout: post
title: Provide context for code
subtitle: June 2025
tags: [published-code-critique, readme, documentation]
author: Faith Okamoto
---

I have today off so I figured I'd do a blog post. Thought I could trust *Nature*
to have some nice code for me to look at. Given the quality of the code for the
first paper I clicked on, perhaps I'd do better to focus on computational
journals in the future...

This month's paper: Hallett EY *et al.* Major expansion in the human niche 
preceded out of Africa dispersal. *Nature* 2025. 
doi: [10.1038/s41586-025-09154-0][DOI]

## Original code

This paper's code is in [three][Code1] [different][Code2] [places][Code3] on
Figshare.

## Critique

The Figshare, as best I can figure<sup>1</sup>, has no README. My feelings about
that are [documented][READMETag]; this paper proves a convenient object lesson
in what happens when code is released into the wild without documentation.

### Where did this data come from?

The [first script][Code1] opens *in media res* with a dataframe being subset. 

```r
# Add other sites  to ROAD database. Once database is complete, subset to only view archaeological deposits that have been chronometrically dated
#filter to see sites directly and chronometrically dated

"enter new dataframe name here" <- subset(Jena_Africa_lithics_10_500ka_EYH_, geological_stratigraphy...11!="geology" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy, geology" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy, stratigraphy" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy, oxygen isotope stratigraphy" & 
  geological_stratigraphy...11!="geology, archaeological (cultural) stratigraphy" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy, geology, stratigraphy" & 
  geological_stratigraphy...11!="geology, oxygen isotope stratigraphy" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy, oxygen isotope stratigraphy" & 
  geological_stratigraphy...11!="archaeological (cultural) stratigraphy, unknown")
```

Yes, that is actually the start of the script. Leaving aside somehow naming a
variable `"enter new dataframe name here"` (which I suspect is unintended?), the 
data is never loaded. Remember, there's no README. I have *no way to know* where 
the data is from.

I'm sure that when the authors ran this script it worked for them. I'm equally
sure that it only worked because they knew what to run prior. 

### Which libraries are required?

Moving on to the [second script][Code2]. At least the data is explicitly loaded
this time. (I'm not immediately sure where the files are from, but maybe they're 
stuffed into a supplement I didn't check.) Scanning down the code, I nodded
along until this jump-scare:

```r
plot2<- ggplot(diff_cal_curves, aes(x, y = Site_and_layer, color = variable)) + 
  geom_point(aes(x = meanage_calibrated, col = "meanage_calibrated"), shape=16, color="black") + 
  geom_point(aes(x = mean_age_opposite_hemisphere_calibration, col = "mean_age_opposite_hemisphere_calibration"), shape=4, color="green") +
  geom_point(aes(x = mean_age_marine_calibration, col = "mean_age_marine_calibration"), shape=3, color="blue") +
  scale_y_discrete(limits=rev) +
  theme(text = element_text(size=3))
```

Wait, what? This script uses [ggplot2][ggplot2]? `library(ggplot2)` is nowhere
to be seen. Even if I tracked down the input files, running this script as-is
*would still error*, due to the missing import statement.

If you're using a library/package/anything, *declare* it.<sup>2</sup> This also
would be ameliorated by a good [README][README]. A "Dependencies" section would 
be enough. (It could even include [version numbers][Versions]!) Instead I'm
forced to reverse-engineer the imports from the code.

### What order do these scripts run in?

I mentioned there were three locations on Figshare. The [first][Code1] seems to 
be meant to run before the [second][Code2], given their names "script 1" and
"script 2" under "[Code availability][CodeAvail]". The [third one][Code3] at 
least has some semblance of order via numbering the scripts. But, when should
the first two be run relative to the third set? Are there cross-dependencies?

Without context, these scripts are like random pages pulled from a book. With
effort one might be able to put them in a logical order, but it is much better
to simply preserve the book's ordering in the first place.

----

There are other issues I have with these scripts (line length is a big one).
However, the micro-level polishing needed pales compared to these macro-scale 
issues. If  a reader has no framework to understand and use your scripts, then 
releasing the  context-less code is, to put it frankly, useless. This paper
makes a joke of *Nature*'s code-release policy.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

----

1. :D  
2. And, hopefully at the start of any relevant script? Many of the scripts in
the [third code dump][Code3] introduce new libraries in the middle of the file,
even if they have a section at the top set aside for preparing the environment.

[Code1]: https://figshare.com/s/d7de3f42aa9e2423bfb5
[Code2]: https://figshare.com/s/291f499a2b7907dfb62b
[Code3]: https://figshare.com/s/3570c73e7a1d6a5e783e
[CodeAvail]: https://www.nature.com/articles/s41586-025-09154-0#code-availability
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1038/s41586-025-09154-0
[ggplot2]: https://ggplot2.tidyverse.org/
[README]: https://www.makeareadme.com/
[READMETag]: https://faithokamoto.github.io/tags/#readme
[Versioms]: https://faithokamoto.github.io/2024-10-06-including-version-numbers/