---
layout: wiki
title: "Linux gcc 链接库"
categolories: Linux, gcc
description: 在Linux中gcc使用了数学函数的源代码需要链接库
keywords: gcc,编译,Linux,库
---

| 序号 | 命令      | 作用       |
| ---- | --------- | ---------- |
| 1    | -lc       | 链接标准库 |
| 2    | -lpthread | 链接线程库 |
| 3    | -lm       | 链接数学库 |

-lm/... 一定要放在待编译源文件后面，否则还是会报错。