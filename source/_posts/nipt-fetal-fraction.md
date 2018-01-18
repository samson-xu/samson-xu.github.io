---
title: NIPT中胎儿染色体含量的计算方法
date: 2018-01-18 10:24:17
tags:
- NIPT
categories:
- BI
comments:
---

# 简介
NIPT(无创产前筛查) ，近年来产前检测领域出现的新型胎儿染色体疾病检测技术，相对传统的绒毛取样或羊膜腔穿刺等具有“侵入性”的产前检测方法而言，其通过高通量测序技术对母亲外周血中的胎儿游离DNA进行“非侵入性”产前检测，开辟了产前检测的新篇章，有效补充了现有的产前筛查、产前诊断体系。该种技术还可以用来评估胎儿染色体的含量。
# 计算公式
```
%chrY = male %chrY x F + female %chrY x (1 - F)
F = (%chrY - female %chrY) / (male %chrY - female %chrY)

%chrY：怀有男性胎儿孕妇外周血中唯一比对到Y染色体上的reads占比对到这个个体reads的比率
male %chrY：男性样本中唯一比对到Y染色体上的reads占比对到这个个体reads的比率
female %chrY：怀有女性胎儿孕妇外周血中唯一比对到Y染色体上的reads占比对到这个个体reads的比率
```
# 注意事项
male %chrY 和 female %chrY的取值，可以根据多个样品计算其中位数得出。
