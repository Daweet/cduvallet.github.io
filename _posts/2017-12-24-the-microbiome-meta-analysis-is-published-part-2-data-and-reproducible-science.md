---
title: 'The microbiome meta-analysis is published, Part 2: Data and reproducible science'
#link: https://claireduvallet.wordpress.com/2017/12/24/the-microbiome-meta-analysis-is-published-part-2-data-and-reproducible-science/
permalink: /posts/2017/12/meta-analysis-is-published-part-2
date: 2017-12-24
tags:
    - publications
---

The other thing I didn't focus on as much in the Nature Microbiology [blog post](https://naturemicrobiologycommunity.nature.com/users/70264-claire-duvallet/posts/22494-beyond-dysbiosis-disease-specific-and-shared-microbiome-responses-to-disease) was all of the lessons I learned about data and doing reproducible science.

It turns out that doing reproducible science is really hard. Making data usefully accessible is not trivial, figuring out how to use someone's else data can be super confusing, and keeping track of what you've done gets unmanageable super quickly.  

Given how hot microbiome research is, when I started this project I thought it'd be super straightforward to gather data from like 100 studies, if not more. After two years of work, I published a paper with data from 28. It turns out that even inclusion criteria as broad as "case-control gut 16S studies" excludes a LOT of studies! Some other common difficulties I encountered, many of which resulted in excluding datasets from my analysis:

  * Data is not uploaded anywhere, so you have to email the authors.
  * Data is uploaded in a database, but it's protected because it contains senstive clinical metadata. This is a problem, because for analyses like mine you'd want to have a way to access the part of the data that isn't protected (e.g. sequencing data and case or control labels, but none of the other more detailed metadata). That said, whether or not microbiome data should be protected is still being [debated](http://www.pnas.org/content/112/22/E2930.full).
  * Data is publicly available, but the metadata is not. A note to all experimentalists: raw data without its metadata is almost always useless.
  * Data and metadata are publicly available, but the IDs don't map between them.
  * Data and metadata are available, but barcodes mapping raw data to samples is not available.
  * Data and metadata are available and mappable, but they don't match what was reported in the paper.
  * Everything is available, but I can't tell what processing steps have been done already. This is actually usually okay - you can just look at the raw data and check, for example, whether primers or barcodes have been removed. However, there was one case where all of the reads were 101 bp but the primers hadn't been removed, and I had no idea why on earth that would be the case.

In addition to feeling like a data detective, there were a few times when I felt like a time traveller:

  * I encountered a handful of hotmail.com and aol.com email addresses in my communications with authors, which always makes me chuckle!
  * It was also interesting that the majority of my datasets were 454 data, whereas the field is now essentially only doing Illumina sequencing. But I think because of how slow academia is, the majority of papers that were out there when I started were from a previous era! It's like the engineers who keep up with the [Voyager satellite](https://www.nytimes.com/2017/08/03/magazine/the-loyal-engineers-steering-nasas-voyager-probes-across-the-universe.html) and still know how to code directly in binary. Okay, it's not like that at all but still!
  * Along those lines, there were a few data formats I encountered that would be ridiculous to have now but which are understandable for studies that were right at the beginning of the NGS boom. For example, quite a few datasets had a subset of their samples in each raw fastq file, but repeated barcodes across files. This meant that the same barcode was in multiple fastq files, but mapped to different samples. Annoying to process, but no biggie.
  * And there was also travelling into the future, when I went to look for data that hadn't been uploaded yet.

I give these examples not to gripe about how everyone sucks at data, but to show that making data usefully available for others to use isn't as straightforward as it sounds! Through my own mistakes in the course of this work, I gained a lot of sympathy (and sometimes empathy) for all the moving parts involved in doing reproducible science.

I made so many mistakes throughout the data processing and analysis. Because I started this project basically as soon as I joined Eric's lab (i.e. before I knew anything about doing computational work), I had to go back and re-do a lot of my data processing - sometimes because I had done it wrong, but most often because I hadn't documented what I did and I couldn't be sure that I hadn't messed it up. In life, I like to try act such that future Claire will think of past Claire and be eternally grateful for her. In life, that means putting a glass of water on my nightstand before going to sleep after a raucous night out. In computational biology, I learned that that means leaving a robust bread crumb trail of READMEs and comments with every data collected and analysis performed.

I also had so many mini-panic attacks where I thought that I had done something completely wrong (like use the wrong statistical test) that would affect all of my other downstream results. If I were a more legit programmer, I would have figured out how to include [unit tests](https://github.com/ericmjl/data-testing-tutorial) throughout my code - though I honestly wonder when this extra effort is worth the benefit, especially in iterative data analyses. [Instead](https://github.com/cduvallet/microbiomeHD), I wrote a Makefile to do all of my analyses so that when I had these doubts it only took an hour or two to resolve them rather than a whole day. You too can perform a broad cross-disease meta-analysis of 28 published case-control gut microbiome studies using standardized methods!

All this to say that I learned to love READMEs and clean code. And some science along the way too, I guess. :)

_Read [Part 1](/posts/2017/12/meta-analysis-is-published-part-1) for an introduction to this post and some personal reflections on publishing the [meta-analysis paper](http://nature.com/articles/s41467-017-01973-8)._
