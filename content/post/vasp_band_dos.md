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
# band
NSW=0    
LCHARG=.TRUE.
```
这里注意INCAR应该加上LCHARG=TRUE: 后面计算能带时需要读取CHARG文件。
如果要进行Dos计算，LORBIT=10用于计算LDOS，LORBIT=11用于计算PDOS。一般选择LORBIT=11计算PDOS，以获得更细致的分析。


# 3.能带(band)的计算
读入上一步的CHGCAR，进行非自洽计算:把INCAR，POTCAR， POSCAR，CHGCAR拷贝过来。

INCAR需要修改的参数
```
ISTART=1
ICHARG=11
LCHARG=F
ISMEAR=0

# dos
EMAX =    输出能量的最大值。
EMIN =    输出能量的最小值。
ENDOS =1001   在能量范围内取数值点的个数，影响DOS的精确度。建议选择较大的值，如果计算结构过于粗糙，也可以尝试增加ENDOS以获得更精确的DOS结果。
LORBIT = 11
```
准备高对称点KPOINTS，因为能带结构就是在高对称点的连线上的能级，所以先前使用的五行式就不适用了，需要找到计算体系的倒易空间的高对称点路径。
利用vaspkit可以很方便得到高对称点路径，生成的高对称点路径在KPATH.in文件里，将其复制成为 KPOINTS即可开始非自洽计算。


