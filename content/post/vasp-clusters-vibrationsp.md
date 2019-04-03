---
title: "团簇振动频率谱的vasp计算"
date: 2018-07-31T01:37:56+08:00
lastmod: 2018-10-08T01:37:56+08:00
draft: false
tags: ["vasp","团簇",“振动谱”,“频率"]
categories: ["vasp"]
author: "qiusb"
---

对于含有N个原子的团簇，平动有三个自由度，一般情况下，转动也有三个自由度，剩余3N-6自由度属于振动。
（可参考朗道《力学》$24）
vasp计算团簇是加真空层把团簇当做晶体计算，故其计算结果是3N个转动频率，若结构优化比较好（稳定），会出现6个接近零的频率（或实或虚）。（许多情况下可当做零处理）
# 计算步骤：
1.结构优化计算（迟豫计算）
INCAR_R
```
SYSTEM=name
NSW=200
ENCUT=400
ISMEAR=0
EDIFFG=-0.02
EDIFF=1e-06
NPAR=2
ISIF=2
ISTART=0
IBRION=2

```
和普通晶体结构优化无区别。


2.计算频率
利用上一步得到的优化后的结构CAONTCAR当做这一步的POSCAR计算频率
INCAR_V
```
SYSTEM=name
NSW=300
ENCUT=400
ISMEAR=0
EDIFFG=-0.01
LCHARG=F
LWAVE=F
LREAL=F
EDIFF=1e-06
#NPAR=2
ISIF=2
IBRION=5
NFREE=2
POTIM=0.02
```
最主要差别在于后三个参数设置，详情参照vasp manual。


注意，NSW的值必须大于3Ｎ*NFREE＋１(+-dx dy dz)！！！

NPAR必须是默认等于核数（不设置）；ENCUT要测试；LREAL可根据情况设为Auto。

！！！真空层大小要慎重，计算速度差距很大。

# 其他：

KPOINTS统一使用gamma点
```
Automatic mesh
0
Gamma
1     1     1
0     0     0


```

任务文件参考
```
申请计算资源的命令



for i in {3..25}
do 
cp INCAR_R INCAR
cp POSCAR-$i POSCAR
mpirun -np ${NSLOTS} vasp5.4.4-std
mv CONTCAR CONTCAR-R$i
mv OSZICAR OSZICAR-R$i
mv OUTCAR OUTCAR-R$i
rm WAVECAR
rm EIGENVAL
cp INCAR_V INCAR
cp CONTCAR-R$i POSCAR
mpirun -np ${NSLOTS} vasp5.4.4-std
mv CONTCAR CONTCAR-V$i
mv OSZICAR OSZICAR-V$i
mv OUTCAR OUTCAR-V$i
rm WAVECAR
rm EIGENVAL
done
```

最后得到的振动盘在OUTCAR里面。采用数据时能量一般使用第一步得到的能量。
附上提取频率和能量命令。
```
grep 'cm-1' OUTCAR >> sp.txt

E=`tail -1 OSZICAR$i`
echo $i$E >>energy
```


