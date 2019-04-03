---
title: "指定能级的电子时空间分布的vasp计算"
date: 2018-10-13T01:37:56+08:00
lastmod: 2018-10-13T01:37:56+08:00
draft: false
tags: ["vasp",“PARCHG”]
categories: ["vasp"]
author: "qiusb"
---

电子密度的时空间分布可以用ＶＥＳＴＡ软件打开CHGCAR(LCHARG=T保留)查看，这里介绍指定能级的电子分布计算。
# 计算步骤：
1.结构优化计算（迟豫计算）
LCHARG=T保留CHGCAR；  LWAVE=T保留WAVECAR
和普通晶体结构优化无区别。


2.计算PARCHG
利用上一步的计算，查看EIGENVAL确定要计算哪些能级的CHG，查看IBZKPT确定计算哪个Ｋ点的CHG。
INCAR_PARCHG
```
system=name
ENCUT=500
ISIF=2
ISTART=1
ICHARG=1
NSW=0
IBRION=-1
EDIFF=1E-5
EDIFFG=-0.01
ISMEAR=0
SIGMA=0.1
NPAR=4
LREAL=Auto
LWAVE=T
LCHARG=T
ALGO=F
IBAND=100 101
KPUSE=1
LPARD=T;LSEPB=T;LSEPK=T

```
IBAND: 指定能级, 在EIGENVAL中找到对应序号。


KPUSE: 指定K点，在IBZKPT中找。


最后一行三个参数是设置分开写PARCHG。


得到的PARCHG文件VESTA打开即可。
