---
title: SAM格式详解
date: 2017-07-19 10:06:41
tags:
- SAM
categories:
- BI
comments:
---
# 简介
SAM是一种序列比对格式标准， 由sanger制定，是以TAB为分割符的文本格式。主要应用于测序序列mapping到基因组上的结果表示，当然也可以表示任意的多重比对结果。


SAM分为两部分，注释信息（header section）和比对结果部分（alignment section），注释信息可有可无，都是以@开头，用不同的tag表示不同的信息，主要有@HD，说明符合标准的版本、对比序列的排列顺序；@SQ，参考序列说明；@RG，比对上的序列（read）说明；@PG，使用的程序说明；@CO，任意的说明信息。
# 比对结果
比对结果部分（alignment section），每一行表示一个片段（segment）的比对信息，包括11个必须的字段（mandatory fields）和一个可选的字段，字段之间用tag分割。必须的字段有11个，顺序固定，不可用时，根据字段定义，可以为’0‘或者’*‘，12个字段详情如下：

|1|QNAME|Query template/pair NAME|
|---|---|---|
|2 | FLAG | bitwise FLAG|
|3 | RNAME | Reference sequence NAME|
|4 | POS | 1-based leftmost POSition/coordinate of clipped sequence|
|5 | MAPQ | MAPping Quality (Phred-scaled)|
|6 | CIGAR | extended CIGAR string|
|7 | MRNM | Mate Reference sequence NaMe ('=' if same as RNAME)|
|8 | MPOS | 1-based Mate POSistion|
|9 | TLEN | inferred Template LENgth (insert size)|
|10 | SEQquery | SEQuence on the same strand as the reference|
|11 | QUAL | query QUALity (ASCII-33 gives the Phred base quality)|
|12 | +OPT | variable OPTional fields in the format TAG:VTYPE:VALUE|

# FLAG详解
Each bit in the FLAG field is defined as:

|0x0001 | p | the read is paired in sequencing|
|---|---|---|
|0x0002 | P | the read is mapped in a proper pair|
|0x0004 | u | the query sequence itself is unmapped|
|0x0008 | U | the mate is unmapped|
|0x0010 | r | strand of the query (1 for reverse)|
|0x0020 | R | strand of the mate|
|0x0040 | 1 | the read is the first read in a pair|
|0x0080 | 2 | the read is the second read in a pair|
|0x0100  |s | the alignment is not primary|
|0x0200 | f | the read fails platform/vendor quality checks|
|0x0400 | d | the read is either a PCR or an optical duplicate|
|0x0800  |S | the alignment is supplementary|

# CIGAR格式
A CIGAR string is comprised of a series of operation lengths plus the operations. The conventional CIGAR format allows for three types of operations: M for match or mismatch, I for insertion and D for deletion. The extended CIGAR format further allows four more operations, as is shown in the following table, to describe clipping, padding and splicing:

|Operation|Description|
|---|---|
|M|Alignment match (can be a sequence match or mismatch)|
|I|Insertion to the reference
|D|Deletion from the reference
|N|Skipped region from the reference
|S|Soft clip on the read (clipped sequence present in <seq>)
|H|Hard clip on the read (clipped sequence NOT present in <seq>)
|P|Padding (silent deletion from the padded reference sequence)
