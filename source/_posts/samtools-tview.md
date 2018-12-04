---
title: samtools下tview命令详解
date: 2017-07-26 11:04:24
tags:
- samtools
categories:
- BI
comments:
---

# tview官方帮助文档
samtools &emsp; tview &emsp;  [-p chr:pos] &emsp; [-s STR] &emsp; [-d display] &emsp; in.sorted.bam &emsp; [ref.fasta]

Text alignment viewer (based on the ncurses library). In the viewer, press '?' for help and press 'g' to check the alignment start from a region in the format like 'chr10:10,000,000' or '=10,000,000' when viewing the same reference sequence.

**Options:**

|**-d** | display | Output as (H)tml or (C)urses or (T)ext|
|---|---|---|
|**-p** | chr:pos | Go directly to this position|
|*-s** | STR |  Display only alignments from this sample or read group|

# 示例

```buildoutcfg
samtools tview -p chr1:10439 *.bam ucsc.hg19.fasta
```
![samtools-tview](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/samtools-tview.jpg)


# viewer参数

|?     |     This window|
|---|---|
| Arrows  |   Small scroll movement|
| h,j,k,l |   Small scroll movement|
| H,J,K,L  |  Large scroll movement|
| ctrl-H   |  Scroll 1k left|
| ctrl-L |    Scroll 1k right|
| space    |  Scroll one screen|
| backspace|  Scroll back one screen|
| g     |     Go to specific location|
| m     |     Color for mapping qual|
| n     |     Color for nucleotide|
| b     |     Color for base quality|
| c     |     Color for cs color|
| z      |    Color for cs qual|
| .     |     Toggle on/off dot view|
| s     |     Toggle on/off ref skip|
| r     |     Toggle on/off rd name|
| N    |      Turn on nt view|
| C   |       Turn on cs view|
| i   |       Toggle on/off ins|
| v     |     Inverse video|
| q   |       Exit|

 >Underline:      Secondary or orphan
 Blue:    0-9    Green: 10-19
 Yellow: 20-29   White: >=30
