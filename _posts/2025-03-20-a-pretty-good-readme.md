---
layout: post
title: A pretty good README
subtitle: March 2025
tags: [published-code-critique, documentation]
author: Faith Okamoto
---

Figured I could do with some praise, and luckily enough, the first manuscript in
[*Bioinformatics*'s "Advance articles"][AdvanceArticles] section fit the bill.

This month's paper: Cousson A *et al.*. NanoASV: a snakemake workflow for
reproducible field-based Nanopore full length 16S Metabarcoding amplicon data
analysis. *G3 Genes|Genomes|Genetics* 2025. doi:
[10.1093/bioinformatics/btaf089][DOI]

## Original code

This paper presents a workflow which they released on [GitHub][Code]. I'm going
to focus on the [README][README], which, for a workflow, is what most people
will look at anyhow.

## Critique

### Use clearly-structured sections

Hallelujah, section headings.<sup>1</sup>

The README is well-formatted with a logical progression of information. At the
top is a summary of the workflow and a copy-paste of the options. Next is how to
install it, presuming the reader liked the summary. Then how to test etc., with
sections later detailing on how everything works and how well it works.

Notice that flow: brief summary, brief how-to-get, brief how-to-use, detailed
what-this-does. That's a good backbone for basically any software's README, in
my book. Using nice headers also means easier linking - always a bonus. I can
read down the page and understand what's happening, or just jump around to the
relevant subsections.

### Explain what example code does

Now for some bad cop. That test code I mentioned? It looks like this:

> ## Test your installation
> 
> ### With a dry run
> 
> ```sh
> nanoasv --dry-run
> ```
> 
> ### With mock dataset
> 
> ```sh
> nanoasv --mock
> ```
>
> You can inspect NanoASV's output structure in `./Mock_run_OUPUT/`.

So, uh, what do these do? How are they different? How much resources (time,
memory) should I expect them to take? Do I do only one, or do I do both? If I do
both, do I have to do anything in between?

The answers to these questions are probably obvious to someone who's used the
software for some time. However, the target audience for a section labeled "Test
your installation" is, by definition, new to the workflow. Thus it would behoove
this section to have some explanation. Any explanation, really. Even a note that
more details can be found in a different section would be an improvement.

### Check the preview

This README is written in [Markdown][Markdown]<sup>2</sup>. That means it
(probably) wasn't typed in a WYSIWYG (What You See Is What You Get) editor. 
Markdown has some little surprises for folks used to WYSIWYG. For example,

```md
First line
Next line
```

would be rendered as

> First line
> Next line

That is, the newline is ignored. (There are ways around this - chiefly, putting
two spaces at the end of a line to force a linebreak). This has legitimate uses.
For example, I typically break up paragraphs into 80 character lines, for easier
reading of the source file, while maintaining a single paragraph in the render.

Because Markdown isn't WYSIWYG, it's important to check what you, well, get.
That means sticking it in some tool that can preview Markdown renders, such as
GitHub or VS Code<sup>3</sup>.

Why do I mention all of this? Because there are some pretty clear instances
where that rule wasn't followed. For example,

```md
Directly input your `/path/to/sequence/data/fastq_pass` directory
4000 sequences `fastq.gz` files are concatenated by barcode identity to make one `barcodeXX.fastq.gz` file.
```

is rendered with just a space between "directory" and "4000", so they look like
they're from the same sentence. At the least, they could've put a period after
"directory" - a copy-editor's eyes would catch the slip with the render.

----

In conclusion, this is a README with great structure and more or less fine
content, but with areas for improvement on presentation.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

----

<sup>1</sup> I do volunteer copyediting. I've seen all sorts of formatting.  
<sup>2</sup> Same as this blog, actually. I type in my VS code with a preview on
the side.  
<sup>3</sup> I also use Stack Exchange's [question editor][AskQuestion] because
I like the buttons.

[AdvanceArticles]: https://academic.oup.com/bioinformatics/advance-articles
[AskQuestion]: https://meta.stackexchange.com/questions/ask
[Code]: https://github.com/ImagoXV/NanoASV
[CV]: https://faithokamoto.github.io/cv/
[DOI]: https://doi.org/10.1093/bioinformatics/btaf089
[Markdown]: https://www.markdowntutorial.com/
[README]: https://github.com/ImagoXV/NanoASV/blob/main/README.md