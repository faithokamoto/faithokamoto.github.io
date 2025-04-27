---
layout: post
title: Format your code
subtitle: April 2025
tags: [published-code-critique, style]
author: Faith Okamoto
---

I'm running out of time for this month's [published-code-critique][CritiqueTag]. Luckily, *Nature*'s front page had this gem: a paper literally referring back to
the days of Mendel<sup>1</sup>! 

This month's paper: Feng C *et al.*. Genomic and genetic insights into Mendel’s
pea genes. *Nature* 2025. doi: [10.1038/s41586-025-08891-6][DOI]

## Original code

This paper's code is on [GitHub][Code].

## Critique

### Be specific about dependencies

Off the main through-line of this post, but I had to mention it. The directory
[README][README] is decent at describing the steps at a high level. That is part
of my [system for directory READMEs][DirectoryREADMEs]. However, there's a major
omission: a list of dependencies. Just this line:

> Most scripts need to be run in a Linux/Unix environment and depend on common bioinformatics tools.

Except... what exactly are "common bioinformatics tools"? Those differ wildly by
sub-field. Even if I knew the tools, which [versions numbers][VersionNumbers]
were used? Any change to any tool might break the scripts.

I understand it's annoying, but a key part of making reproducible code is
documenting version numbers.

### Use line breaks

The README says to run things in order, so I'm going to the first file:
`00.SNP_calling_and_QC/00.QC2fastq.sh`. One line is *over 300 characters*:

```bash
#!/bin/bash

for sample in $(cat zz_samle.list); do
    echo "fastp -i ${sample}_1.fastq.gz -I ${sample}_2.fastq.gz -o ${sample}_1.fastp.fastq.gz -O ${sample}_2.fastp.fastq.gz --adapter_sequence=AGTCGGAGGCCAAGCGGTCTTAGGAAGACAA --adapter_sequence_r2=AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTA -w 5 -f 5 -F 5 -l 80 -g -j ${sample}.json -h ${sample}.html" > "${sample}.fastp.sh"
done
```

You don't need to limit your files to [79 characters][Pep8LineLength], but
there's a limit. This is *well* over it. There is no reasonable way to read the
whole line at once. Even auto-wrapping has a tendency to mess code up visually.
If the statement needs to be that long, please for the love of readability use
line breaks. For example:

```bash
#!/bin/bash

for sample in $(cat zz_samle.list); do
    echo "fastp -i ${sample}_1.fastq.gz -I ${sample}_2.fastq.gz \
        -o ${sample}_1.fastp.fastq.gz -O ${sample}_2.fastp.fastq.gz \
        --adapter_sequence=AGTCGGAGGCCAAGCGGTCTTAGGAAGACAA \
        --adapter_sequence_r2=AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTA \
        -w 5 -f 5 -F 5 -l 80 -g \
        -j ${sample}.json -h ${sample}.html" > "${sample}.fastp.sh"
done
```

Voila, everything is readable. Lne-breaks also break it up into sub-sections
(e.g. input arguments here, output arguments there).

Beyond the line break issue, I'm not sure what this is doing? I can see it's
sending a `fastp` command to a file, but why these specific arguments? Another
benefit of breaking up a long line: each part could get an explanatory comment.

## Use indentation

On to the next script, `00.SNP_calling_and_QC/01.fastq2gvcf.sh`. Line lengths
are shorter (the longest is "only" around 200 characters) but there is a new 
readability issue: indentation. Specifically, indentation within blocks:

```bash
for library in `grep $sample sample_lib.list | cut -f 2 -d ","`;
do

fq1=$data_path/$sample/${sample}_${library}_1.fastp.fastq.gz
fq2=$data_path/$sample/${sample}_${library}_2.fastp.fastq.gz
group=$library
platform="ILLUMINA"
bam_option="--bam_compression 1"

echo "time ( $sentieon_path/bin/sentieon bwa mem -M -R '@RG\tID:$group\tPL:$platform\tLB:$library\tSM:$sample' -t $nt \
-K 10000000 $ref_genome $fq1 $fq2 || echo -n 'error' ) | $sentieon_path/bin/sentieon util sort $bam_option \
-r $ref_genome -o ${sample}.${library}.sort.bam -t $nt --sam2bam -i -
">>${sample}/${sample}.sentieon.sh
all="$all ${sample}.${library}.sort.bam"
done

multi=2
runs=$(grep $sample sample_lib.list | cut -f 2 -d ","|wc -l)
if [ $runs -ge $multi ];then

echo "samtools merge -@ $nt ${sample}.sorted.bam $all && rm $all ${all}.bai

samtools index -@ $nt ${sample}.sorted.bam
" >>${sample}/${sample}.sentieon.sh
else

echo "mv ${sample}.${library}.sort.bam ${sample}.sorted.bam
rm ${sample}.${library}.sort.bam.bai
samtools index -@ $nt ${sample}.sorted.bam
" >>${sample}/${sample}.sentieon.sh
fi
```

Where does the `for` loop start and end? How about the `if` statement, and its
`else` block? Are there any blocks nested inside of either of those?

Some code viewers will make this a little easier to scan by e.g. using colors.
Even then it's a difficult. But there's a simple, better way:

```bash
for library in `grep $sample sample_lib.list | cut -f 2 -d ","`;
do

    fq1=$data_path/$sample/${sample}_${library}_1.fastp.fastq.gz
    fq2=$data_path/$sample/${sample}_${library}_2.fastp.fastq.gz
    group=$library
    platform="ILLUMINA"
    bam_option="--bam_compression 1"

    echo "time ( $sentieon_path/bin/sentieon bwa mem -M -R '@RG\tID:$group\tPL:$platform\tLB:$library\tSM:$sample' -t $nt \
    -K 10000000 $ref_genome $fq1 $fq2 || echo -n 'error' ) | $sentieon_path/bin/sentieon util sort $bam_option \
    -r $ref_genome -o ${sample}.${library}.sort.bam -t $nt --sam2bam -i -
    ">>${sample}/${sample}.sentieon.sh
    all="$all ${sample}.${library}.sort.bam"
done

multi=2
runs=$(grep $sample sample_lib.list | cut -f 2 -d ","|wc -l)
if [ $runs -ge $multi ];then

    echo "samtools merge -@ $nt ${sample}.sorted.bam $all && rm $all ${all}.bai

    samtools index -@ $nt ${sample}.sorted.bam
    " >>${sample}/${sample}.sentieon.sh
else

    echo "mv ${sample}.${library}.sort.bam ${sample}.sorted.bam
    rm ${sample}.${library}.sort.bam.bai
    samtools index -@ $nt ${sample}.sorted.bam
    " >>${sample}/${sample}.sentieon.sh
fi
```

See how much easier this is to scan? Even a cursory glance reveals the basic
block structure, and it's easy to know what is inside of what.

Some programming languages (*cough cough* Python) enforce indentation. Many
don't. Still, you should always use proper indentation. It has massive
readability benefits, especially with more complicated block structures. With a
few levels of nesting and few sub-blocks per level, the reader will be lost fast 
without indentation as an anchor and guide for the eye<sup>2</sup>.

----

Those two latter sections are the big things. Glancing through some of the other
scripts, I have quibbles (e.g. the Python ones lack spaces after the commas in
function calls, and have generally inconsistent whitespace). However, those pale
in comparison to the massive readability issues caused by failing to indent and
failing to use line breaks. Please format your code, y'all. You have to read it
too.

If there's a recent paper you'd like me to look through, shoot me an email.
Address in my [CV][CV].

----

<sup>1</sup> The brief bit of Mendelian genetics I learned in 9th grade is why I
started focusing on biology.  
<sup>2</sup> I have to admit I have no idea how this works for people who rely
on [screen readers][ScreenReaders].

[CritiqueTag]: https://faithokamoto.github.io/tags/#published-code-critique
[Code]: https://github.com/ShifengCHENG-Laboratory/MendelPeaG2P
[CV]: https://faithokamoto.github.io/cv/
[DirectoryREADMEs]: https://faithokamoto.github.io/2025-04-19-directory-readmes/
[DOI]: https://doi.org/10.1038/s41586-025-08891-6
[Pep8LineLength]: https://peps.python.org/pep-0008/#maximum-line-length
[README]: https://github.com/ShifengCHENG-Laboratory/MendelPeaG2P/blob/main/README.md
[ScreenReaders]: https://www.afb.org/blindness-and-low-vision/using-technology/assistive-technology-products/screen-readers
[VersionNumbers]: https://faithokamoto.github.io/2024-10-06-including-version-numbers/