---
layout: post
title: Do a final cleanup
subtitle: December 2024
tags: [published-code-critique, last-pass]
author: Faith Okamoto
---

I've blathered on for ten posts about *my* code habits. Now I'll look at other 
scientists' code. This blog post is the first of a series. Once a month, I'll 
critique the code released by a recent paper. Hopefully concrete examples will
make clear principles I've discussed.

This month's paper:
Bornbusch, SL *et al*. Fecal microbiota transplants facilitate
post-antibiotic recovery of gut microbiota in cheetahs (*Acinonyx jubatus*).
*Commun Biol* 2024. doi: [10.1038/s42003-024-07361-5][DOI]

## Original code

The [archive][Files] for this paper only have a [single code file][Code]. I 
think all the interactive code was just copied into a single script. If there 
was a last pass for readability etc. then it leaves a lot to be desired.

Since there's too much code to review in full I'll pull bits from the start.

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Kill absolute paths with fire

```r
#Laptop
setwd("~/Dropbox (Personal)/Microbiome_SLB/Smithsonian/POSTDOC_RESEARCH/CHFMT_SCBI_cheetahs ABX/DATA/R")

#work desktop & home desktop
setwd("~/Dropbox/Microbiome_SLB/Smithsonian/POSTDOC_RESEARCH/CHFMT_SCBI_cheetahs ABX/DATA/R")
```

These paths are useful for exactly no one but the code's developer. What's more,
having two of them is unnecessarily confusing. The code you release doesn't have
to be exactly what you ran. It should be *what others can run* to reproduce your
results.

In this case, a better alternative would be a clearly defined directory
structure. For example, a [README][README] which explains how code files, data,
results etc. [should be organized][Organize]. 

### Organize your imports

```r
library(lme4)
library(lmerTest)
library(phyloseq)
library(tidyr)
library(biomeUtils)
library(MASS)
library(dplyr)
library(coda4microbiome)
library(vegan)
library(emmeans)
library(multcomp)
library(biomeUtils)
library(mgcv)
library(visreg)
library(reshape)
library(compositions)
library(biomformat)
library(microViz)
library(FEAST)
library(biomformat)
library(ggpicrust2)
library(readr)
library(KEGGREST)
library(ggpubr)
library(gridExtra)
library(decontam)
```

This is a mess. It's difficult to easily see  which libraries are included. I 
usually alphabetize my imports, but another option is to separate them into 
chunks (e.g. labeled `# graphing utilities`, `# phylogenetics`).

### Use logical groupings

```r
#load final ASV table
otu_mat <- read.csv(file="chfmt_table5_decontam.csv") 
otu_mat <- otu_mat %>%
  tibble::column_to_rownames("ASV_ID")

#load final taxonomy table 
tax_mat <- read.csv(file="chfmt_taxonomy_decontam.csv")
tax_mat <- tax_mat %>%
  tibble::column_to_rownames("Feature_ID")

#load metadata
meta <- read.csv(file="chfmt_mappingfile_decontam.csv")
meta <- meta %>%
  tibble::column_to_rownames("SampleID")
attach(meta)

otu_mat <- as.matrix(otu_mat)
tax_mat <- as.matrix(tax_mat)
```

Don't force readers to hold many ongoing things in memory at the same time. 
When I hit the `as.matrix()` lines, I'd honestly forgotten those variables were 
created right before `meta`. While the coder may have converted to a matrix 
after loading the CSVs, when organizing code for public release, it makes more 
sense to create the "final" `otu_mat` and `tax_mat` variables all at once. 
Thus, moving the `as.matrix()` lines to the `read.csv()` block.

In addition, the [`read.csv()` function][ReadDoc] has a way to specify row names
(`row.names=`) in the same statement as the filename, which I would've done for
the same principle of combining related things.

### Double-check lines which output results

```r
## phylogenetic tree imported from QIIME2
## filtered to include the 2558 ASVs minus the "unknowns"
phy_tree_filt <- phyloseq::read_tree("chfmt_unrooted-tree.nwk")
#ggtree(phy_tree_filt, layout="circular") #+ 
#geom_text(aes(label=label), size=3, color="purple", hjust=-0.3)

otu = otu_table(otu_mat, taxa_are_rows = TRUE)
taxonomy = tax_table(tax_mat)
metadata = sample_data(meta)
#DNAseqs = readDNAStringSet("old_analyses/PmLong_feature_DNAsequence.fasta")

taxa_names(taxonomy)
taxa_names(otu)
```

Is that `ggtree()` plot used in the paper? Then it should be uncommented, since 
a reproducer would run it. (A comment indicating the specific figure wouldn't
go amiss.) Then, the `taxa_names()` lines. Are they output? I don't know. If 
they are, then I'd like a comment indicating what to focus on. If not, then a 
comment for what they do.

As an aside unrelated to the subheading, what's going on with that middle block?
Why does it have `=` instead of `<-` for assignment? Does this script use their 
[subtle differences][AssignOp]? Or is this just an instance of nonuniform code 
style? I, the reader am confused. I'm extra confused by the `DNAseqs` line.
That variable seems to be used nowhere else. Before archiving code, please
remove any lines which are no longer relevant.

----

Later issues in the code are either repeats or somewhat unrelated to this post's
throughline of making sure to reorganize code before archival. Check back next
month to see me do this again. If there's a recent paper you'd like me to look
through, shoot me an email. Address in my [CV][CV].

[AssignOp]: https://stackoverflow.com/questions/1741820/what-are-the-differences-between-and-assignment-operators
[Code]: https://osf.io/8s76q
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1038/s42003-024-07361-5
[Files]: https://osf.io/sp7kx/files/osfstorage
[Organize]: https://faithokamoto.github.io/2024-11-16-organizing-files/
[README]: https://www.makeareadme.com/
[ReadDoc]: https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/read.table