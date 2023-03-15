---
layout: post
title: "第一周C语言力扣题"
categories: C
description: 游戏部布置的第一周的Leetcode题
keywords: leetcode,刷题
---

# 罗马数字转阿拉伯数字

  这是一道力扣的简单题，但以我数组和指针都没学过临时看了一下数组的水平，实际上是很有难度的。

  好在我室友有一个数组指针都学了的，所以在他的帮助下，我还是成功写出来了(计算阿拉伯数字是我自己设计的，他教了我怎么求数组的元素数目。)

  我看了数组之后以为是要自己声明数组然后将像从键盘输入一样全部读入数组，然后室友告诉我char *s,这里的s就是数组。可以直接拿来用。

## 1,计算数组元素个数

  首先这一题先要求数组的元素个数，后面才好设计循环结构来将罗马数字变成阿拉伯数字  

```c
int romanToInt(char * s)
{
    int n=0, ret=1, i=0, number=0;
    while(ret==1)
    {
        n++;
        ret = scanf("%c",&s[n]);
    }
    while(i<=n)
    {
        if(s[i]== 'I'&&(s[i+1]=='V'||s[i+1]=='X'))
            number--;
        else if(s[i]== 'I')
             number++;
        if(s[i]== 'V')
                number += 5;
        if(s[i]== 'X'&&(s[i+1]== 'L'||s[i+1]== 'C'))
            number -= 10;
        else if(s[i]== 'X')
            number += 10;
        if(s[i]=='L')
            number += 50;
        if(s[i]=='C'&&(s[i+1]=='D'||s[i+1]=='M'))
            number -= 100;
        else if(s[i]='C')
            number += 100;
        if(s[i]== 'D')
            number += 500;
        if(s[i]== 'M')
            number += 1000;                             
            
        
    }
    return 0;
    
}
```

  这是我第一次写时一次性写出来的东西，写的真的很垃圾，而且最后写的居然是return 0,然后代码执行出来是时间超出限制。

![1](https://i.loli.net/2021/11/07/xOARrv14LW2CtgE.png)

  然后力扣的debug要充会员，不能直接调试找错。

  因此我就先把后面的计算过程都删了，来先看求数组元素个数是否出错

```c
int romanToInt(char * s)
{
    int n=0, ret=1, i=0, number=0;
    while(ret==1)
    {
        n++;
        ret = scanf("%c",&s[n]);
    }
    
    return n;
}

```

![2](https://i.loli.net/2021/11/07/YBoGmDS9hPvcNxe.png)

  然后这里就出问题了，循环是根本不会继续进去的。室友说scanf只能是从键盘输入数据,然后getchar也是从键盘，所以这两个都没用。

  接下来我在网上搜了一下该怎么求数组的元素个数，基本上都是用sizeof(数组名)/sizeof(数组名[0])，原理挺好理解的，然后我就用了。

  ![图床突然服务器端出错](https://pic.imgdb.cn/item/6187650f2ab3f51d91472f5c.png)

  结果让我懵了,我试了另外几个用例，毫无例外输出都是8，我完全搞不懂了用sizeof为什么不行。我又找了我室友帮忙，他说s前面有*所以这是指针，传过来的是地址，虽然可以直接当成数组用，但指针占用内存是8字节。

  最后室友提示我每个数组结尾都是\0，比如字符串实际上就是字符数组，最后都有一个系统编译器自动补足的\0

  利用这一点我总算是成功地把计算数组的元素个数给写出来了。

  ![4](https://pic.imgdb.cn/item/6187668b2ab3f51d91491724.png)

## 2，罗马数字转成阿拉伯数字的运算设计

  这个地方难点是4,9等这样的数字。把I放在V的左边是5-1=4而不是5+1=6。在题目中把所有的这种情况都列出来了，在循环中单独列出来就行然后把加改成减就行。

```c
int romanToInt(char * s)
{
    int n=0, i=0, number=0;
    while(s[n]!='\0')
    n++;
     while(i<=n)
    {
        if(s[i]== 'I')
        {
            if(s[i+1]=='V'||s[i+1]=='X')
                number--;
            else
                number++;
        }
        else if(s[i]=='V')
            number += 5;
        else if(s[i]=='X')
        {
            if(s[i+1]=='L'||s[i+1]=='C')
            number -= 10;
            else
            number += 10;
        }
        else if(s[i]=='L')
            number += 50;
        else if(s[i]=='C')
        {
            if(s[i+1]=='D'||s[i+1]=='M')
            number -= 100;
            else
            number += 100;
        }
        else if(s[i]=='D')
            number += 500;
        else if(s[i]=='M')
            number += 1000;    
        i++;
    }          
        return number;
}
```

​    ![](https://pic.imgdb.cn/item/6187692c2ab3f51d914c0590.png)



  至此终于是写完了

