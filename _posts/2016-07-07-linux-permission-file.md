---
title:  Linux 给文件及文件夹附权限
author: fengxw
tag: [linux]
---

权限有三种类型，r（读）、w（写）、x（执行），且每种类型有对应的值：

```
r=4
w=2
x=1
```

文件权限由三组 rwx 组成：

```
xxx xxx xxx
按从左到右，分别是文件所属用户，文件所属用户组，所有用户
```

赋值的时候按所需权限的值求和：

```
-rw-r--r-x   chmod -R 645  file(dir)
```