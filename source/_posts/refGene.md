---
title: refGene文件解析
date: 2018-05-15 15:52:20
tags:
- refGene
categories:
- BI
comments:
---

# 简介
RefGene数据库是从UCSC数据库创建而来。RefGene指定了取自NCBI RNA参考序列集合（RefSeq）的已知人类蛋白质编码和非蛋白质编码的基因，用于注释变异基因。
hg19 RefGene 下载方式：
```
wget http://hgdownload.cse.ucsc.edu/goldenpath/hg19/database/refGene.txt.gz
```
# 文件解析
以下是对RefGene文件各列内容的详细说明
> START:0-based
> END:1-based
```
1. bin，索引域，数据库中用来加速查询染色体的分布
2. name，NM accession number，标志基因各个转录本的ID，即mRNA或lncRNA的ID（通常来自于GTF中的转录本ID）
3. chrom，基因所在的染色体号
4. strand，数据库中对该基因收录的方向
5. txStart，基因的起点，从转录起始位点开始
6. txEnd，基因的终点，转录时最后3'UTR最后一个已知碱基的位置
7. cdsStart，编码区的起点，即主要开放阅读框的起点
8. cdsEnd，编码区的终点，即主要开放阅读框的终点
9. exonCount，该转录本的外显子个数
10. exonStarts，每一个外显子的起点集合
11. exonEnds，每一个外显子的终点集合（一定与Exon_start的坐标个数一致）
12. score，得分
13. name2，基因ID
14. cdsStartStat
15. cdsEndStat
16. exonFrames
```

# 文件示例
```
585     NR_148357       chr1    +       11868   14362   14362   14362   3       11868,12612,13220,      12227,12721,14362,      0       LOC102725121    unk     unk     -1,-1,-1,
585     NR_046018       chr1    +       11873   14409   14409   14409   3       11873,12612,13220,      12227,12721,14409,      0       DDX11L1 unk     unk     -1,-1,-1,
```

# 基因示意图
![gene_structure](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/gene_structure.png)

# 成熟mRNA示意图
![mRNA_structure](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/mRNA_structure.png)
