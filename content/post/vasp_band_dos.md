---
title: "vasp计算能带和态密度"
date: 2024-03-05T01:37:56+08:00
lastmod: 2024-03-05T01:37:57+08:00
draft: false
tags: ["vasp","Band","Dos"]
categories: ["vasp"]
author: "qiusb"
---

# 1.弛豫结构



# 2.自洽计算(scf)
将弛豫后结构作为输入POSCAR，进行静态计算：
```
NSW=0    

LCHARG=.TRUE.
```
这里注意INCAR应该加上LCHARG=TRUE: 后面计算能带时需要读取CHARG文件。



# 3.能带(band)的计算
读入上一步的CHGCAR，进行非自洽计算:把INCAR，POTCAR， POSCAR，CHGCAR拷贝过来。

INCAR需要修改的参数
```
ISTART=1
ICHARG=11
LCHARG=F
ISMEAR=0
```
准备高对称点KPOINTS，因为能带结构就是在高对称点的连线上的能级，所以先前使用的五行式就不适用了，需要找到计算体系的倒易空间的高对称点路径。
利用vaspkit可以很方便得到高对称电路径，生成的高对称点路径在KPATH.in文件里，将其复制成为 KPOINTS即可开始非自洽计算。


