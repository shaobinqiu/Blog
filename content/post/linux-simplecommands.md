---
title: "Linux Simplecommands"
date: 2018-08-03T09:54:13+08:00
lastmod: 2018-08-03T10:54:13+08:00
draft: false
tags: ["linux", "command"]
categories: ["linux"]
author: "qiusb"
---

# linux简单命令

cp 多个文件文件：

```
cp /home/usr/dir/{file1,file2,file3,file4} /home/usr/destination/
```

cp 拥有共同前缀文件:

```
cp /home/usr/dir/file{1..4} ./
```




查看可导入模块：

```
module avail
```

导入模块：

```
module load modulename
```

查看已导入模块：
```
module list
```