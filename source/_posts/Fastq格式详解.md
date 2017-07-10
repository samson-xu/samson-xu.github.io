---
title: Fastq格式详解
date: 2017-07-10 16:05:41
tags:
- Fastq
categories:
- BI
comments:
---

FASTQ是基于文本的，保存生物序列（通常是核酸序列）和其测序质量信息的标准格式。其序列以及质量信息都是使用一个ASCII字符标示，最初由Sanger开发，目的是将FASTA序列与质量数据放到一起，目前已经成为高通量测序结果的事实标准。

# 格式说明

**FASTQ文件中每个序列通常有四行：**
>1. 序列标识以及相关的描述信息，以‘@’开头；
>2. 第二行是序列
>3. 第三行以‘+’开头，后面是序列标示符、描述信息，或者什么也不加
>4. 第四行，是质量信息，和第二行的序列相对应，每一个序列都有一个质量评分，根据评分体系的不同，每个字符的含义表示的数字也不相同。


**例如：**
@SEQ_ID
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT
+
!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65


# 旧版reads name

@HWUSI-EAS100R:6:73:941:1973#0/1

HWUSI-EAS100R: the unique instrument name
6: flowcell lane
73: tile number within the flowcell lane
941: ‘x’-coordinate of the cluster within the tile
1973: ‘y’-coordinate of the cluster within the tile
\#0: index number for a multiplexed sample (0 for no indexing)
/1: the member of a pair, /1 or /2 (paired-end or mate-pair reads only)



# 新版reads name
@EAS139:136:FC706VJ:2:2104:15343:197393 1:Y:18:ATCACG

EAS139: the unique instrument name
136: the run id
FC706VJ: the flowcell id
2: flowcell lane
2104: tile number within the flowcell lane
15343: ‘x’-coordinate of the cluster within the tile
197393: ‘y’-coordinate of the cluster within the tile
1: the member of a pair, 1 or 2 (paired-end or mate-pair reads only)
Y: Y if the read fails filter (read is bad), N otherwise
18: 0 when none of the control bits are on, otherwise it is an even number
ATCACG: index sequence


# 文件后缀

没有特别的规定，通常使用.fq, .fastq, .txt等