

## Docker搭建LNMP实验

在腾讯云实验室进行了通过docker搭建好LNMP的教程，如果只是顺着手册步骤cv一遍，那么基本上记不住什么东西，而且理解也很浅。所以写一篇博客确实是可以巩固所学习的内容，以后有所遗忘也能够到博客看一看。

### Docker的安装

![腾讯云实验](https://pic.imgdb.cn/item/6231493f5baa1a80ababa54a.png)

mkdir 命令我还是很熟了，用来创建文件夹。但~/我却从来都没用过，不知道什么意思。上网查询得知其等效于 home/用户名。sudo命令是使用root权限进行这项命令，安装东西一般都要root权限。如果本身已经使用sudo su进入了root模式，那么其它命令前面就不用打sudo。我经常使用apt安装软件，不常用apt-get。实际上我也不清楚apt-get是什么，以前我有搜索过，但又不记得了。apt在我的理解里像是软件商店，ubuntu的默认软件商店是apt，centos的默认软件商店是yum。这个 -y 我只知道是某个附加的选项，但我不知道是什么意思，也许是安装最新版的意思。上网查询原来是yes的意思，很简单的用法。很多软件安装时都会问是否安装该软件(y n),加-y就不会再问了，直接安装

所以这一段的命令意思是 创建一个docker文件夹，进入docker文件夹，在此文件夹内安装docker的核心文件



![image-20220316104131509](https://pic.imgdb.cn/item/62314e8a5baa1a80abadd17a.png)

  **从网上摘的笔记**

### 更换镜像源

![](https://pic.imgdb.cn/item/623150075baa1a80abaebed9.png)

Docker的工作基础是镜像，镜像是啥之前我是完全不懂。但做上次作业体验了一下进入Docker镜像，感觉跟虚拟机很像，镜像和我实际的系统互不干扰，我在镜像中新建的东西不会出现在我的系统中。国内访问Docker Hub很慢，所以需要更换为国内的镜像源地址。

我曾经做过cat的笔记，最基本用法就是查看文件内容，我只会这个用法，其他用法都没掌握。

但是这个地方还是可以理解的。

新建或者只是打开写入(我不知道这里是哪种情况，也不知道cat能不能新建文件) /etc/docker/damon.json下面大括号里的内容，注册镜像:要替换的国内镜像源地址，打EOF表示退出写入。然后重启docker，退出root。

![](https://pic.imgdb.cn/item/623153de5baa1a80abb16953.png)

  **我的笔记**

### 下载需要用到的Docker镜像

![](https://pic.imgdb.cn/item/6231540e5baa1a80abb18aca.png)

Docker使用docker pull <镜像>来完成镜像的下载工作，这个用法与git一致，git push将本地文件夹上传至网络仓库，git pull将网络仓库内文件下载至本地文件夹。我们一般说的LNMP指的就是Linux,Nginx,mySQL,PHP。腾讯的这个实验使用了PostgreSQL代替mySQL。sudo docker image ls查看已下载的镜像。而sudo docker pull nginx:alpine 即为安装nginx镜像，但是alpine不知道是什么，初次接触我猜是版本。

上网查了一下果然是版本，alpine相比于latest有几点优势:

1.用的是最新版nginx镜像，功能与nginx:latest一模一样

2.alpine镜像使用的是Alpine Linux内核，比ubuntu内核小很多

3.nginx:alpine默认支持http2

![](https://pic.imgdb.cn/item/623162415baa1a80abbc55d2.png)

**网上摘的笔记**

PHP和PostgreSQL的下载也和nginx一样。

php:7-fpm-alpine

postgres:alpine

### 启动和停止Nginx

![](https://pic.imgdb.cn/item/623162bd5baa1a80abbcc53f.png)

使用docker run来启动容器，各种参数图片里都有解释。



![](https://pic.imgdb.cn/item/6231638f5baa1a80abbdb4d4.png)

所有的命令都是相通的，ls在linux是查看目录下的文件的意思，在这里sudo docker container ls就可以查看所有容器及其ID。sudo docker stop <容器ID或容器名称>就能停止一个容器。

### 启动LNMP

![](https://pic.imgdb.cn/item/623167535baa1a80abc0838f.png)

LNMP有三个容器，单个启动麻烦，所以使用docker-compose管理并启动它们

先安装python-pip,我是这么理解的:pip的用法与apt-get类似，apt里没有docker-compose，所以我们要先下载python-pip。

或许docker-compose就是一个python脚本，而python-pip就是脚本管理工具，其内置脚本市场。

#### 创建docker-compose配置文件并编辑

![](https://pic.imgdb.cn/item/62316c575baa1a80abc44064.png)



使用touch命令在docker文件夹下创建文件docker-compose.yml，这是我此次学到的新命令

![](https://pic.imgdb.cn/item/62316e005baa1a80abc5602f.png)

![](https://pic.imgdb.cn/item/62316e195baa1a80abc5719b.png)

这个地方是难点，我最初是手打了一遍，结果代码有出入，导致后面的步骤出问题。后面还有好几个这样的要编辑文件的，然后我就cv了。除了直接打开文件写还可以在终端使用vim编辑。这里配置文件里的内容相比于上面的命令还是要复杂一些，看下面的说明也看得懂，但这样不能算是掌握了。

```bash
version: "3"
services:

  Nginx:
    image: nginx:alpine
    ports:
      - 80:80
    volumes:
      - ./web:/usr/share/nginx/html:ro
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro

  PHP:
    image: undefined01/php:7-fpm-alpine
    volumes:
      - ./web:/var/www/html:rw

  Database:
    image: postgres:alpine
    environment:
      POSTGRES_USER: "postgres"
      POSTGRES_PASSWORD: "rootroot"
    volumes:
      - ./data:/var/lib/postgresql/data:rw
```

#### 创建Nginx配置文件并编辑

![](https://pic.imgdb.cn/item/62316fb95baa1a80abc6b0c4.png)

同样使用touch在docker文件夹下创建nginx.conf

![](https://pic.imgdb.cn/item/623170335baa1a80abc6fb68.png)

编辑的nginx.conf内的内容我是不懂的，考着我的垃圾英语勉强能理解，但是还是一样，这并不能算掌握。



```bash
server {
    listen       80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.php index.html index.htm;
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    location ~ \.php$ {
        fastcgi_pass   PHP:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  /var/www/html/$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```

#### 使用docker-compose启动服务

![](https://pic.imgdb.cn/item/623171415baa1a80abc795d0.png)

使用 sudo docker-compose up -d来启动三个容器。sudo docker container ls可以查看已经启动的容器。

### 测试LNMP环境

![](https://pic.imgdb.cn/item/623173925baa1a80abc905d5.png)

使用sudo chmod -R 777 ./data ./web获取编辑权限。

或者sudo su直接进入root模式

### 测试PHP

![](https://pic.imgdb.cn/item/623174895baa1a80abc99c82.png)

使用touch创建index.php

![](https://pic.imgdb.cn/item/623174be5baa1a80abc9bfa7.png)

```
<?php
phpinfo();
?>
```

仍然是不怎么懂得文件内容

### 测试PostgreSQL

![](https://pic.imgdb.cn/item/623175495baa1a80abca17fd.png)

![](https://pic.imgdb.cn/item/623175825baa1a80abca38c1.png)

```
<?php
$dbconn = pg_connect('host=Database user=postgres password=rootroot') or die('Could not connect: ' . pg_last_error());
pg_query('CREATE TABLE IF NOT EXISTS test ( tester INT )');

pg_query('INSERT INTO test VALUES (0)');
$res = pg_query('SELECT * FROM test') or die('Query failed: ' . pg_last_error());
$num = pg_num_rows($res);
echo "You have visited this site $num times";

pg_free_result($res);
pg_close($dbconn);
?>
```

基本差不多的操作

### docker-compose停止服务

![](https://pic.imgdb.cn/item/623175c65baa1a80abca5fd4.png)

测试结束，到这整个一套流程就结束了



做完实验后，我想自己在电脑的虚拟机vm Linux上试一下，然后vm提示更新，我更新了。结果电脑就出问题了，桌面一直无限刷新，cpu直接跑满。搞了几个小时搞好后，vm 里的Linux启动不了了。我就删了vm准备用wsl，结果电脑装wsl也出问题，一直报错。(我在室友电脑上帮他装好了wsl2，但我自己电脑上却装不好，新版自动安装和旧版手动安装都试过)。现在呢甚至vm安装包都打不开。我的电脑系统一定是出了什么问题，做完最近的作业就重装系统。

---

## 不使用Docker搭建LNMP

![](https://pic.imgdb.cn/item/6231c2865baa1a80ab06c2cf.png)

这个实验是在cenots下完成的，我想跟ubuntu下也差不多，无非是yum变成apt

### 搭建Nginx静态服务器

#### 安装Nginx

![](https://pic.imgdb.cn/item/6231c32b5baa1a80ab07dd4a.png)

在cenots中是使用yum安装nginx，并且不需要sudo，-y放在了最后面

#### 修改配置

![](https://pic.imgdb.cn/item/6231c4d75baa1a80ab0b42c8.png)

打开 /ect/nginx/conf.d/default.conf去除对IPv6的监听，修改成一下代码

```bash
server {
    listen       80 default_server;
    # listen       [::]:80 default_server;
    server_name  _;
    root         /usr/share/nginx/html;

    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }

}
```

实际上只需修改第三行：在listen前面加个#

#### 启动Nginx

![](https://pic.imgdb.cn/item/6231c5f75baa1a80ab0d5906.png)

输入nginx直接可以启动nginx，使用chkconfig打开nginx的开机自动启动

#### 安装MySQL

![](https://pic.imgdb.cn/item/6231c68e5baa1a80ab0e793a.png)

安装都大同小异，只要知道要安装的东西的名字，使用yum install 名字就可以。 安装好之后设置开机自动启动，重启mysql并设置root密码。

### 搭建PHP环境

#### 安装PHP

![](https://pic.imgdb.cn/item/6231c7645baa1a80ab1010cc.png)

这里grep命令用于查找文件里符合条件的字符串

![](https://pic.imgdb.cn/item/6231c8255baa1a80ab1155d3.png)

### 配置Nginx并运行PHP程序

#### 配置php.conf

![](https://pic.imgdb.cn/item/6231c8935baa1a80ab120c2d.png)

```
server {
    listen 8000;
    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ \.php$ {
        root           /usr/share/php;
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```

listen是监听的意思，listen 8000即监听8000端口

#### 重启nginx

![](https://pic.imgdb.cn/item/6231c90e5baa1a80ab12e161.png)

#### 配置info.php

![](https://pic.imgdb.cn/item/6231c9665baa1a80ab13757f.png)

在使用Docker的实验中也有这一步

做完这一步，不依赖Docker的LNMP就搭建好了

