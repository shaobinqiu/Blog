---
title: "分子Raman spectrum的vasp计算"
date: 2021-06-01T01:37:56+08:00
lastmod: 2021-06-01T01:37:57+08:00
draft: false
tags: ["vasp",“Raman”]
categories: ["vasp"]
author: "qiusb"
---

# 1.优化弛豫结构


# 2.[计算分子的声子](https://shaobinqiu.github.io/post/vasp-clusters-vibrationsp/)

这里注意INCAR应该加上NWRITE=3: 后期计算介电响应时读取文件要求。



# 3.Dielectric Tensor的计算

INCAR
```
ENCUT = 600
EDIFF = 1e-6
ISMEAR = 0
SIGMA = 0.05
POTIM = 0.1
LCHARG = FALSE
LWAVE = FALSE
IBRION=6
ISIF=3
NFREE=4
EDIFFG = -0.001
```
关键参数:  将IBRION=6；ISIF=3；NFREE=4；

不能设置NPAR， 不然会报错：
```
ERROR
|      VASP internal routines  have requested a change of the k-point set.    |
|      Unfortunately this is only possible if NPAR=number of nodes.           |
|      Please remove the tag NPAR from the INCAR file and restart the         |
|      calculations.                                                          |
```


弹性矩阵会直接写在OUTCAR里。


计算得到的elastic moduli 是直角坐标下的，只要在同一直角坐标下，不同取lattice，结果相同。测试过diamond的pcell和supercell。


pcell
```

 TOTAL ELASTIC MODULI (kBar)
 Direction    XX          YY          ZZ          XY          YZ          ZX
 --------------------------------------------------------------------------------
 XX       10531.4122   1243.9931   1243.9931      0.0000     -0.0000     -0.0000
 YY        1243.9931  10531.4122   1243.9931      0.0000      0.0000      0.0000
 ZZ        1243.9931   1243.9931  10531.4122      0.0000     -0.0000      0.0000
 XY           0.0000      0.0000      0.0000   5628.7346      0.0000      0.0000
 YZ          -0.0000      0.0000     -0.0000      0.0000   5628.7346     -0.0000
 ZX          -0.0000      0.0000      0.0000      0.0000     -0.0000   5628.7346
 --------------------------------------------------------------------------------


```


supercell
```
 TOTAL ELASTIC MODULI (kBar)
 Direction    XX          YY          ZZ          XY          YZ          ZX
 --------------------------------------------------------------------------------
 XX       10534.8952   1243.0926   1243.0926      0.0000      0.0000      0.0000
 YY        1243.0926  10534.8952   1243.0926      0.0000      0.0000     -0.0000
 ZZ        1243.0926   1243.0926  10534.8952      0.0000     -0.0000      0.0000
 XY           0.0000      0.0000      0.0000   5629.8633      0.0000     -0.0000
 YZ           0.0000      0.0000     -0.0000     -0.0000   5629.8633     -0.0000
 ZX           0.0000     -0.0000      0.0000     -0.0000     -0.0000   5629.8633
 --------------------------------------------------------------------------------
```
实验数据参考： https://doi.org/10.1063/1.4704698
