---
title: "conda"
date: 2018-09-04T09:54:13+08:00
lastmod: 2018-09-04T10:54:13+08:00
draft: false
tags: ["linux", "conda"]
categories: ["conda"]
author: "qiusb"
---

# conda


## 1.创建环境
```
conda create -n name [dependent package list]
```


例如
```
conda create -n pyyabc python=3.6
```


## 2.激活失效环境

```
source activate name
source deactivate
```


## 3.列出环境
```
conda info --envs
```
带*为当前环境


## 4.删除环境
```
conda remove -n name --all
```
