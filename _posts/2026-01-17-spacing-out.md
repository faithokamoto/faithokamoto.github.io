---
layout: post
title: Spacing out
subtitle: please do
tags: [published-code-critique, whitespace, readability]
author: Faith Okamoto
---

I have a draft of the Introduction section of my qualifying exam! To celebrate,
here's a code critique of one of the papers I'm citing.

This month's paper: Xu P. *et al.* ClipSV: improving structural variation 
detection by read extension, spliced alignment and tree-based decision rules
*NAR Genomics and Bioinformatics* 2021. doi: [10.1093/nargab/lqab003][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

*Standard disclaimer: issues with published code are not necessarily anyone's
fault, and often are due to nothing more nefarious than time constraints.*

### Use blank lines between sections

In [`clipsv_scripts/breakpoint_candidate.py`][bp_can] I was greeted by this
lovely scene:

```py
#!/usr/bin/env python
import subprocess,sys,os,shutil

def breakpoint_candidate(chromosome,bam,genome_fa,genome_mmi,coverage,min_insert_size,max_insert_size,read_length):
	fold=int(round(float(coverage)/10))
	root_path=os.getcwd()
	os.chdir(chromosome+"_dir")
	path=os.getcwd()
	clips=chromosome+"_clips"
	indel=chromosome+"_indel"
	overlapping=chromosome+"_clips_overlapping"
	from breakpoint_candidate_scripts.indel_filter import indel_filter
	indel_filter(indel,int(fold))
```

And it goes on and on. The only blank lines are in between functions. This is
simply unreadable. It becomes a "wall of text"; I see the giant mass of writing
and my eyes start to glaze over. It would be much easier to understand if split
up into subsections. For example:

```py
#!/usr/bin/env python
import subprocess,sys,os,shutil

def breakpoint_candidate(chromosome,bam,genome_fa,genome_mmi,coverage,min_insert_size,max_insert_size,read_length):
	fold=int(round(float(coverage)/10))

    # Build file names
	root_path=os.getcwd()
	os.chdir(chromosome+"_dir")
	path=os.getcwd()
	clips=chromosome+"_clips"
	indel=chromosome+"_indel"
	overlapping=chromosome+"_clips_overlapping"

	from breakpoint_candidate_scripts.indel_filter import indel_filter
	indel_filter(indel,int(fold))
```

See how I even put a comment to start a major block of code? By splitting off
those filename lines into their own little section, and labeling that section,
it is now easier to scan the overall structure and understand what's happening.

### Put imports together

You may have noticed something else unusual in that last bit I quoted: an
`import` statement within a function. While this is possible in Python, its
_good_ uses are rather limited. For example, if you write a large script which
can produce a plot as a minor functionality, it might make sense to put the
`import matplotlib` statement inside of the plotting function. Then, anyone who
wants to only use the non-plotting capabilities doesn't have to worry about the
plotting dependencies.

That is not the case here.

```py
	from breakpoint_candidate_scripts.indel_filter import indel_filter
	indel_filter(indel,int(fold))
	split=chromosome+"_split"
	from breakpoint_candidate_scripts.split_duplication import split_duplication
	split_duplication(split)
	from breakpoint_candidate_scripts.merge_split_duplication import merge_split_duplication
	merge_split_duplication(split+".duplication",int(fold))
	from breakpoint_candidate_scripts.combine_SV import combine_SV
	combine_SV(clips+".filter.SV",overlapping+".filter.SV",indel+".filter.SV",split+".duplication.merge.SV","combined_SV")
	from breakpoint_candidate_scripts.combine_indel import combine_indel
	combine_indel(clips+".filter.INDEL",overlapping+".filter.INDEL",indel+".filter.INDEL",split+".duplication.merge.INDEL","combined_INDEL")
	from breakpoint_candidate_scripts.remove_redundancy import remove_redundancy
	remove_redundancy("combined_INDEL")
	remove_redundancy("combined_SV.deletion")
	remove_redundancy("combined_SV.insertion")
```

Yes, you're reading that correctly. This script continuously imports functions
from other files _right before use_. Despite the larger `breakpoint_candidate()`
function being the only thing one could even do with this file. There's no use
that doesn't require importing these things, so just put them at the top!

To tie this back in to spacing: if the imports are at the top, they can be
organized into thematic groups. With newlines, or at least comments, in between.
This allows for a reader to see at a glance what this file uses. As-is I have
to pick out all the `import` lines smushed within the morass of that function.

### But what is this doing?

The nigh-unreadable code and confused import statements contribute to another
problem: I have no earthly idea what this script is doing. The README doesn't go
file-by-file (reasonable; there are many files) and the file itself doesn't
provide comments or [script docstrings][ScriptDocBlog]. Which means that without
a lot of concerted effort by me to step through this paper's code, it is
effectively a black box.

We're scientists, folks, not magicians. I know there's a paper with the method.
But if I want to understand how that method was implemented, I want a clear
understanding of file dependencies (i.e. organized import statements) and a
clear structure for each file (i.e. whitespace). Got it?

---

These are by no means all the problems. The same issues as came up in my prior
["Format your code"][FormatBlog] (and the first of the subheadings from 
["Examining demo code samples"][DemoBlog]) are present here, too. But you don't 
need me to rewrite my old posts :D I'll see y'all around some bad code later.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

[bp_can]: https://github.com/ChongLab/ClipSV/blob/master/clipsv_scripts/breakpoint_candidate.py
[Code]: https://github.com/pxulab/ClipSV
[CV]: https://faithokamoto.github.io/cv/
[DemoBlog]: https://faithokamoto.github.io/2025-10-12-examining-demo-code-samples/
[DOI]: https://doi.org/10.1093/nargab/lqab003
[FormatBlog]: https://faithokamoto.github.io/2025-04-26-format-your-code/
[ScriptDocBlog]: https://faithokamoto.github.io/2024-09-24-script-docstrings/