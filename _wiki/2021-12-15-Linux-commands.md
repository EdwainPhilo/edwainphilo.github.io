---
layout: wiki
title: "Linux 命令"
categories: Linux
description: 本人的命令积累笔记
keywords: Linux,command,命令,不完整
---

| 命令                                                        | 作用                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| --save-temps                                                | gcc保存编译过程中的中间文件                                  |
| mv test.txt wbk.txt                                         | 将test.txt重命名为wbk.txt                                    |
| mv /usr/udt/* .                                             | 将/usr/udt中的所有文件移动到当前目录                         |
| mv * ../                                                    | 将当前文件夹下的所有文件移动到上一级目录                     |
| mmv (-n) f\\* F\\#1                                         | 将所有以f开头的文件改成以F开头,中间的-n表示打印输出而不是重命名文件,用于重命名前检验一下。 |
| mmv (-n) \\*.c \\#1.txt                                     | 将后缀名为.c的后缀名全部修改为.txt                           |
| mmv (-n) '*abc\*' '#1xyz#2'                                 | 将文件名中带有abc的文件的abc全部改为xyz,前后的字符数可以不相等 |
| mmv f\\* ..                                                 | 将所有以f开头的文件移动到上一级目录                          |
| man mmv                                                     | mmv的详细使用说明                                            |
| mv 文件名/* 另一个目录                                      | 把当前目录的一个子目录里的文件移动到另一个子目录里           |
| sudo su                                                     | 进入root                                                     |
| sudo passwd root                                            | root模式下修改root密码                                       |
| poweroff                                                    | 关机                                                         |
| tail [参数] [文件]                                          | 查看文件的内容 参数:  -f 循环读取 -q 不显示处理信息 -v 显示详细的处理信息 -c<数目>     显示的字节数 -n<行数>     显示文件的尾部 n 行内容 --pid=PID     与-f合用,表示在进程ID,PID死掉之后结束 -q, --quiet,     --silent 从不输出给出文件名的首部 -s,     --sleep-interval=S 与-f合用,表示在每次反复的间隔休眠S秒 |
| more [-dlfpcsu] [-num] [+/pattern] [+linenum] [fileNames..] | Linux more 命令类似 cat ，不过会以一页一页的形式显示，更方便使用者逐页阅读，而最基本的指令就是按空白键（space）就往下一页显示，按 b 键就会往回（back）一页显示，而且还有搜寻字串的功能（与 vi 相似），使用中的说明文件，请按 h 。 |



