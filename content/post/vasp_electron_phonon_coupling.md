---
title: "电声耦合强度的vasp计算"
date: 2018-10-15T01:37:56+08:00
lastmod: 2018-10-15T01:37:56+08:00
draft: false
tags: ["vasp",“electron-phonon coupling”]
categories: ["vasp"]
author: "qiusb"
---

利用vasp可以得到特征频率\omega_i，得到的hessian matrix 和 eigenvalue and eigenvectors of hessian matrix都在vasprum.xml里面（文件后部分）。


eigenvectors 为行向量。


方法是先按照eigenvector的模式来移动原子（设置最大的移动距离某一数值，例如0.05埃），然后电子步自恰迭代得到总能和能级的变化。


INCAR参考：
```
NSW=0
ENCUT=400
ISMEAR=0
EDIFFG=-0.01
LREAL=Auto
EDIFF=1e-06
NPAR=4
IBRION=-1

```
