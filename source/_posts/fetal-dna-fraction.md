---
title: 孕妇外周血中胎儿游离DNA浓度测定方法
date: 2019-12-27 14:35:48
tags:
- 游离DNA
categories:
- BI
comments:
---

无创产前检测（NIPT）在临床获得了广泛应用，其理论基础是孕妇的外周血中存在胎儿游离DNA（cell-free fetal DNA, cffDNA）。应用NIPT进行胎儿染色体非整倍体检测时，cffDNA浓度过低会导致假阴性的发生，因此cffDNA浓度≥4%被认为是一个重要质控指标；此外，在无创单基因病检测中，对cffDNA浓度的准确估算也尤为重要，cffDNA浓度是分析位点变异的重要参数。那么cffDNA的浓度到底该如何计算呢？下图列举了几种cffDNA浓度估算的方法。

![fetal-dna-fraction](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fetal-dna-fraction.png)
<center> **cffDNA浓度估算方法**

## Y染色体估算法
![fdf-a](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fdf-a.png)

**原理：**根据母体血浆总DNA中男胎Y染色体片段所占比例计算cfDNA浓度

**优点：**简单；准确

**缺点：**不适用于女胎

##  基于SNP的胎儿特异SNP位点法
![fdf-b](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fdf-b.png)

**原理：**选取母亲为纯合，胎儿为杂合的位点，估算cfDNA浓度。比如父亲的基因型为CC，母亲为AA，则胎儿为CA，胎儿特异性位点C的比例可以估算cfDNA浓度

**优点：**直接；准确

**缺点：**父亲DNA有时获取存在困难

##  基于SNP的深度靶向测序法（FetalQuant）
**原理：**将孕妇外周血中的cfDNA看成复合基因型（AAAA，AAAB，ABAA，ABAB，每组前两个字母代表母亲基因型，后两个下标代表胎儿基因型），应用最大似然数估算法，估算cfDNA浓度。该方法能够通过母亲外周深度测序的结果分析出母亲纯合而胎儿杂合的SNP位点

**优点：**只需要检测母体血浆DNA；准确

**缺点：**需要深度测序

##  基于SNP 的低深度测序（FetalQuantSD）
**原理：**该方法是FetalQuant的改进方法，先用微阵列芯片对母亲外周血进行基因分型，获得母亲纯合的SNP位点，血浆DNA中不同于母亲的SNP位点则为来自于父亲的SNP位点，即为胎儿特异SNP位点，可以估算cfDNA浓度 

**优点：**只需要对母体血浆DNA低深度测序；准确

**缺点：**母亲基因分型需要额外成本；不同的基因分型和测序平台需要重新校准曲线

##  基于cfDNA片段数目（seqFF）
![fdf-c](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fdf-c.png)

**原理：**对血浆单端测序后，划分成50kb的bins，建立高维回归模型（high-dimensional regression model），分析获得结果

**优点：**只需要对母体血浆进行测序；单端测序；易于整合到现有的NIPT流程中

**缺点：**需要大样本来建立网络模型；当cfDNA浓度低于5%时准确性差 

##  基于甲基化标记的方法
![fdf-d](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fdf-d.png)

**原理：**胎儿DNA甲基化与母亲DNA甲基化程度不同，甲基化测序区分胎儿和母亲来源的DNA 

**优点：**准确 

**缺点：**测序前用亚硫酸盐或者对甲基化敏感的酶切处理可能降低准确性；甲基化测序成本较高 

##  基于cfDNA长度差异
![fdf-e](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fdf-e.png)

**原理：**根据cfDNA片段较母体游离DNA片段短，建立回归模型分析

**优点：**只需要对母体血浆进行低深度测序；易于整合到现有的NIPT流程中

**缺点：**准确性一般；双端测序增加成本 

##  基于核小体印迹法
![fdf-f](https://blog-1256671606.cos.ap-guangzhou.myqcloud.com/picture/fdf/fdf-f.png)

**原理：**研究发现核小体核心序列部分占所有核小体序列比例与cfDNA浓度有一定的相关性 

**优点：**测序深度低 

**缺点：**准确性差；在构建模型时需要进行深度测序

一个快速、简单、准确、经济的cffDNA浓度估算方法对NIPT来说是非常必要的，特别是针对NIPT的未来发展方向——无创单基因病的临床应用来说尤为重要。cffDNA浓度会影响NIPT结果的准确性，此外，还具有潜在的临床诊断价值：cffDNA浓度与妊娠结局相关，比如cffDNA浓度低可能与胎盘小或者胎盘异常相关。目前，上述提到的基于片段长度、数目、核小体图谱等方法对低浓度cffDNA的准确估算，还需要大样本的研究。此外，也有研究发现血浆DNA里面片段末端具有来源（母亲或者胎儿）偏好性，可以根据片段末端特征判断DNA片段来源，从而估算cffDNA浓度。

相信随着研究的深入，cffDNA的生成机制和cffDNA浓度的影响因素会得到阐明。我们期待cffDNA浓度估算方法能够取得更多突破，从而促进NIPT的发展，也为临床诊断妊娠相关疾病提供更多有益参考。

>参考文献：Xianlu Laura Peng；Peiyong Jiang. Bioinformatics Approaches for Fetal DNA Fraction Estimation in Noninvasive Prenatal Testing. Int. J. Mol. Sci. 2017, 18, 453
