---
layout: post
title: "rnm!Linux:Linux Ubuntu20.04改为竖屏后鼠标移位导致无法改回来的解决方法"
categories: Linux
description: 将Linux的显示方向改为向右旋转后导致鼠标移位无法改回原本的正常显示的解决方法
keywords: Linux,竖屏,鼠标移位
---

# LinuxUbuntu屏幕向右旋转后鼠标移位导致无法改回原本显示方式的解决办法

  今天下午我在修改显示百分比，然后比较好奇最上面的那个选项是什么意思(英语有点差)。试过之后就知道是什么了。然后我就点了这个Portrait Right。

![](https://pic.imgdb.cn/item/6194b1272ab3f51d9150bf34.png)

  然后屏幕就向右旋转了。这本来也没什么。看到是竖屏之后我就想改回去，点击Revent Settings就能回到原来的设置。但我发现我怎么都点不了这个，无奈我就点了Keep Change。这个时候还没意识到是鼠标错位的问题

![](https://pic.imgdb.cn/item/6194b2002ab3f51d91518b83.png)

  我想再次更改设置然后发现鼠标不对劲(截图没办法截下光标)，我的光标在靠近顶部的地方，产生反应的地方(是那个Appearance变黑了)在底部。我怎么也没法点到上面的选项。

![](https://pic.imgdb.cn/item/6194b2ac2ab3f51d9151f477.png)

  鼠标没用就用键盘，我开始用键盘来选择，结果到应用新设置时不管我按方向键上下左右都无法将光框移到Apply。

![](https://pic.imgdb.cn/item/6194b3f72ab3f51d91528959.png)

  我大骂LinuxUbuntu的开发者为什么在最后这一步用不了键盘了。暴躁地敲击键盘。

  骂归骂我不想重装系统，所以还是上网去查解决方法。

  我在csdn上搜到了一个解决ubuntu触摸板旋转后触控不准问题的帖子，按照上面的步骤把脑袋也向右旋转90度在终端打上一串串代码。结果到打的配置文件无法保存退出。

  RNM Linux

  我知道我只有一个方法了，就是使用终端命令来旋转屏幕。

  最后终于找到了旋转屏幕的命令:

| xrandr -o normal                          | 恢复默认方向                   |
| ----------------------------------------- | ------------------------------ |
| xrandr -o left                            | 左旋转                         |
| xrand -o q                                | 查看当前显示器的输出信息       |
| xrand --output HDMI1 --rotate left/normal | 旋转某个视频接口的视频输出方向 |
| xrand --help                              | 帮助                           |

----

最后我实际上也找到了用键盘恢复的方法，就是在这个界面用按tab能将光框移动到Apply

![](https://pic.imgdb.cn/item/6194b3f72ab3f51d91528959.png)
