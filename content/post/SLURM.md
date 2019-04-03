---
title: "SLURM"
date: 2018-09-11T15:07:34+08:00
lastmod: 2018-09-11T15:54:13+08:00
draft: false
tags: ["linux", "SLURM"]
categories: ["SLURM"]
author: "qiusb"
---

# SLURM

## 1. 任务提交

```
sbatch job.sh
```

## 2. 任务查询

查看用户任务

```
squeue
```

任务状态

PD    排队等待


R     运行


S     挂起


F     失败结束


CA    取消


TO    超时


NF    节点故障

## 3. 任务删除

```
scancel jobnumber #任务号可以通过squeue看到
```

## 4. 查看计算资源

```
sinfo
```
分区和时间上限都可以看到

# 任务脚本参考

job.sh

```
#!/bin/bash -l
# NOTE the -l flag!
#
#SBATCH -J NAME
# Default in slurm
# Request 5 hours run time
#SBATCH -t 5:0:0
#
#SBATCH -p small -N 1 -n 12
# NOTE Each small node has 12 cores
#

module load vasp/5.4.4-impi-mkl

# add your job logical here!!!
mpirun -n 12 vasp_std       
```

 more SLURM:


 https://research.computing.yale.edu/support/hpc/user-guide/slurm


 https://hpcc.usc.edu/support/documentation/slurm/
