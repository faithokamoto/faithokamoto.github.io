---
layout: post
title: Crediting sources in your code
subtitle: Not just about plagiarism
tags: [comments]
author: Faith Okamoto
---

I've been copying code from other sources for some recent scripting. Copy-paste
is an incredible time-saver. (Provided it's used well, i.e. you double-check the
code and understand what it does.) Another best practice, or at least a practice
recommended by me, is to credit sources in your code.

## What's a source?

No, not [source code][SourceCode]. I mean the sources your code is based on.

- **Copy-paste** sources. If you take a loop from [Stack Overflow][BashLoop]:
    ```bash
    # Based on https://stackoverflow.com/a/1521498/
    while IFS="" read -r gene || [ -n "$gene" ]
    do
        python code/myscript.py $gene
    done < data/chosen_genes.txt
    ```
    This doesn't require an exact copy-paste. Note the names and loop body 
    differ from the link. Still, the structure of the loop is from the link.
- **People** you took code from. If you use a co-worker's script as an example:
    ```bash
    # RSID annotation from Faith Okamoto
    bcftools annotate -a data/dbSnp155Common.sorted.bed.gz \
        -c CHROM,FROM,TO,RSID,REF,-,ALT -O z $prefix.vcf.gz > $prefix.annotated.vcf.gz
    ```
- **Standards** the code is written for. A VCF-writing script might 
link the [VCF specification][VCF]:
    ```python
    # VCF format: https://samtools.github.io/hts-specs/VCFv4.2.pdf
    snps = snps[['#CHROM', 'POS', 'ID', 'REF', 'ALT', 'QUAL', 'FILTER', 'INFO']]
    with open(file, 'w') as vcf:
        vcf.write(f'##fileformat=VCFv4.2\n##contig=<ID={CHR_NAMES[chrom]}>\n')
        snps.to_csv(vcf, sep='\t', index=False, lineterminator='\n')
    ```

## Why link sources?

Well, are you going to remember the source?

That's the core issue. By relying on an external resource, you outsource the 
documentation. You don't need to write exactly what `|| [ -n "$gene" ]` does, 
because the link already explains. You don't need to justify each column in a
VCF, because it's in the spec. 

But what if you need to modify that bash loop? What if you need to figure out
why the regex you hacked together for the `INFO` column stopped working? Then
you want to trace how you made the code.

If you wonder what `-` means in `-c CHROM,FROM,TO,RSID,REF,-,ALT`, the comment 
tells you who put it in there. If you read someone else's code and don't 
immediately see why `##contig=<ID={CHR_NAMES[chrom]}>\n` is necessary, the VCF 
spec link is your first port of call.

Be kind to your future self. Do you really want to spend an hour digging up the 
obscure forum post which explains how some script gets around an old software's 
bug? Probably not. By curating links and sources within your code, you *vastly* 
simplify the process of looking up the relevant sources later.

[BashLoop]: https://stackoverflow.com/a/1521498/
[SourceCode]: https://www.geeksforgeeks.org/difference-between-source-code-and-object-code/
[VCF]: https://samtools.github.io/hts-specs/VCFv4.2.pdf
