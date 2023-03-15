---
layout: post
title: "Github博客图片无法加载出来的一种解决方案"
categories: Github
description: Typora搭配Github图床上传撰写文档
keywords: PicGo, Github, 图片
---

  作为一个萌新，在写完第一个博客后就发现图片加载不出来（胡鸽鸽在网课中没讲），在网上寻找了一番找到了一个合理方便的让图片加载出来的

# 通过github+picgo搭建图床来解决(注意picgo是外国图床工具,仍然需要科学上网或者连接校园网加载图片)

## 1，创建Personal access token

  点击github头像--Settings-- Developer settings--Personal access tokens，创建一个新的tokens，勾选repo，note随便打,Expiration选no expiration,拉到最后面创建。

  ![example](https://i.loli.net/2021/10/20/G5LgCEW1m4PXowy.png)

![next](https://i.loli.net/2021/10/20/Kcem6bfFnotkO71.png)

  点击创建后，此处会显示token，先复制贴到其他地方去，后面用得上，此处只会显示这一次。

![next](https://i.loli.net/2021/10/20/TuhMS5AzoOtyqvY.png)

## 2,PicGo的安装

   PicGo安装地址:[Release 2.3.0 · Molunerfinn/PicGo (github.com)](https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.0)

​    选择仅为我安装,然后一路点击下一步

![example](https://i.loli.net/2021/10/20/fHtixaTnKgDAkV7.png)

  打开PicGo,点击图床设置，GitHub图床

![next](https://i.loli.net/2021/10/20/FvI1iOT5ZqN9gBb.png)

仓库名：github账号/刚新建的仓库名

设定分支名：master或main 具体到github仓库中查看此处

![next](https://i.loli.net/2021/10/20/J2A6mah1IDgYBuy.png)

设定的tokens:就是第一步新建的token，粘贴到此处

指定存储路径：就是将来图片需要存放的路径，可随便填写，此处img/

将来图片默认上传的路径就为img/xxxx.jpg

我的自定义域名:https://raw.githubusercontent.com/Philonb/Philo.github.io/master

自定义域名格式:http://raw.githubusercontent.com/你的github用户名/你的仓库名/分支名

全部填写完之后，点击确定。

在点击PicGo上传区选择Markdown，然后随便拖一个图片上来到Github图传，看能否上传成功。

![next](https://i.loli.net/2021/10/20/UPSguzNXqDOjEIi.png)

![next](https://i.loli.net/2021/10/20/G2DYpNQRlWAvz8C.png)

提示上传成功即可，如中途进度条显示红色，上传失败的话，可尝试重启PicGo软件再试，若一直失败，可返回检查图床设置，token，分支等信息是否填写错误。

## 3,Typora的设置

打开Typora,点击文件，偏好设置，图像

![image-20211020195033931](https://i.loli.net/2021/10/20/oUtQNu7XAep4mZY.png)

插入图片时那里选择上传图片，勾选对本地位置的图片应用上述规则。上传服务选择PicGo(app),手动选择PicGo路径，如果不知道就在桌面右击PicGo图标选择属性,将目标里的东西复制粘贴到PicGo路径

![next](https://i.loli.net/2021/10/20/5XpqHh6beOLvwES.png)

  完成后截一张图贴到md文件中，可以发现此时图片正在上传，上传完成后发现图片路径为url地址而不是跟之前一样的为本地计算机绝对路径。

![next](https://i.loli.net/2021/10/20/iH3tpN5CVrvmyPK.png)

后续如需删除图片只需在PicGo相册中删除即可。

至此Typora图床搭建完毕