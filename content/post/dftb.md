---
title: "DFTB+"
date: 2018-11-10T01:37:56+08:00
lastmod: 2018-11-11T01:37:56+08:00
draft: false
tags: ["dftb"]
categories: ["dftb"]
author: "qiusb"
---

NFTB+: http://www.dftbplus.org/


案例文件：https://github.com/shaobinqiu/dftb_example


### dftb简单说明
结构文件：sheet文件夹下的geo_start.gen文件。
第一行第一个数值为原子数目  后面字符S代表晶体，需要在最后加上lattice；C代表分子，不需要加lattice。


参数文件：dftb_in.hsd


优化后结构文件：sheet文件夹下的geo_opt.gen和geo_opt.xyz文件。


### 运行命令
```
dftb+ dftb_in.hsd
```
