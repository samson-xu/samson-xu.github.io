---
title: R语言安装包镜像选择
date: 2017-09-11 15:10:26
tags:
categories:
- R
comments:
---

# 简介
使用 Bioconductor 的biocLite()安装程序包时，可能速度很慢，这时可以设定一个国内的镜像（中科大镜像），使用chooseBioCmirror()选择中国镜像即可。
biocLite()通常也需要安装依赖的程序包，这时需要从CRAN下载，默认的CRAN镜像是cran.rstuido.com速度有时也会很慢，可以在安装程序包前先指定CRAN镜像。使用chooseCRANmirror()选择国内镜像即可。

# BioConductor镜像选择
```buildoutcfg
> chooseBioCmirror()
HTTPS BioC mirror 

1: 0-Bioconductor (World-wide) [https]
2: Brazil/Latin America (Ribeirão Preto) [https]
3: Germany (Dortmund) [https]
4: United Kingdom (Hinxton) [https]
5: Japan (Tachikawa) [https]
6: Japan (Wako) [https]
7: China (Anhui) [https]
8: Australia (Sydney) [https]
9: (HTTP mirrors)

Selection: 7
> 
```

# CRAN镜像选择
```buildoutcfg
> chooseCRANmirror()
HTTPS CRAN mirror 

 1: 0-Cloud [https]                   2: Austria [https]                   3: Belgium (Ghent) [https]        
 4: Chile [https]                     5: China (Beijing 4) [https]         6: Colombia (Cali) [https]        
 7: France (Lyon 1) [https]           8: France (Lyon 2) [https]           9: France (Paris 2) [https]       
10: Germany (Münster) [https]        11: Iceland [https]                  12: Italy (Padua) [https]          
13: Japan (Tokyo) [https]            14: Mexico (Mexico City) [https]     15: New Zealand [https]            
16: Russia (Moscow) [https]          17: Spain (A Coru<U+00F1>a) [https]  18: Spain (Madrid) [https]         
19: Switzerland [https]              20: UK (Bristol) [https]             21: UK (Cambridge) [https]         
22: USA (CA 1) [https]               23: USA (KS) [https]                 24: USA (MI 1) [https]             
25: USA (TN) [https]                 26: USA (TX) [https]                 27: USA (WA) [https]               
28: (HTTP mirrors)                   

Selection: 5
>
```