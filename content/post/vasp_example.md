---
title: "15上的vasp计算提交示范"
date: 2018-09-11T18:03:09+08:00
lastmod: 2018-09-11T18:04:09+08:00
draft: false
tags: ["15", "vasp"]
categories: [“vasp”，“15”]
author: qiusb
 
---
为方便零基础的新同学尽快熟悉在集群15上面的vasp计算，这里讲一个简单的计算流程走一遍。
先找管理员要到自己的账号密码。接下来

## 登录集群
windows用户推荐使用cmder软件链接服务器。下载链接：http://cmder.net/
打开软件，在命令行操作
```
ssh username@232.38.220.15
```

linux用户
terminal
```
ssh username@232.38.220.15
```
！！！！！ip改为服务器ip，这里只是示范，不是实际ip。


## bash 修改
对于新用户，使用前需要修改~/.bashrc文件
利用vim对~/.bashrc文件进行编辑，vim用法参考：https://shaobinqiu.github.io/post/vim/
```
vim ~/.bashrc
```
删除原来内容，将下面内容替换原来的./bashrc
```
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# Uncomment the following line if you don't like systemctl's auto-paging feature:                                                                            
# export SYSTEMD_PAGER=

# User specific aliases and functions
ulimit -s unlimited

```
保存退出后
```
source ~/.bashrc
```

这是为了让修改立刻生效。

## 开始使用vasp
15集群赝势文件所在目录：/opt/ohpc/pub/apps/vasp/pps


将自己的计算文件（POSCAR KPOINTS POTCAR INCAR ...）放在一个文件夹下,进入文件夹
```
vim job.sh #创建提交任务脚本
```
将下面内容贴到job.sh中
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
## 提交任务
一切准备就绪后（文件夹下必须文件POSCAR POTCAR INCAR KPOINTS job.sh），可以提交任务。


15集群使用的任务管理系统是SLURM

任务的管理查看SLURM模块：


https://shaobinqiu.github.io/post/slurm/

