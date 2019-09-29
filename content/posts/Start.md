---
title: Hexo 踩坑笔记：利用Hexo和github pages服务搭建个人博客
date: 2017-01-10 17:43:12
updated: 2017-08-06
categories: 
- 技术
tags: 
- Hexo
- Github
---

 > ** 声明：** 
 >  本人是学渣，英语渣，代码渣。能完成此博客并且部署到线上大多依赖于网络上乐于分享的诸多前辈。
 > 在此表示感谢。另外搭建过程中有很多问题我依然一头雾水，各位小伙伴若有高见，还请不吝赐教。再次感谢。

**此文所有设置均在window环境下进行**

<!-- more -->

# 安装Git和node.js

请自行到官网下载，另，请自备梯子。安装基本没什么需要讲的，一路 next 就可以。

[git官网](https://www.git-scm.com/ "git")

[node.js官网](https://nodejs.org/en/ "node.js")

#### 需要学习Git的同学请移步廖雪峰前辈的网站：[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

需要注意的是，在需要用到 `npm` 之前，请切换到国内的淘宝镜像，否则下载速度异常缓慢，导致各种出错。

此处放上[淘宝镜像](https://npm.taobao.org/ "cnpm")的链接。

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

之后在用到 `npm` 的地方只需要换成 `cnpm` 就可以了。

# 安装Hexo
```
$ mkdir hexo 
$ cd hexo 
$ hexo init
```

之后经过了漫长的等待。结果：

![npm error](http://ojp2aqyk4.bkt.clouddn.com/hexo1.jpg "npm error")

没有管这个，继续进行。

``` 
$ cnpm install
$ hexo generate
$ hexo server
```

打开 http://localhost:4000/  ，没反应。

又重新输入了一下`$ hexo init` ， 最后弹出的一行是 `Start Blogging with Hexo !`

再次打开 http://localhost:4000/  ，这次是一直处于刷新的状态，页面却显示不出来。

![http://localhost:4000/](http://ojp2aqyk4.bkt.clouddn.com/hexo2.jpg "")

谷歌了一下说是4000端口被占用。所以输入以下命令改变一下端口：
​    
`$ hexo s -p 2222`

然后从打开 http://localhost:2222/。 终于见到了界面。开心~~

## 几个常用的Hexo命令
```
常用命令：
hexo help     #查看帮助
hexo init     #初始化一个目录
hexo generate #生成静态网页，在 public 目录查看整个网站的文件
hexo server   #本地预览
hexo deploy   #部署.deploy目录
hexo clean    #清除缓存，每次执行命令前先清理缓存，每次部署前先删除 .deploy 文件夹

简写：
hexo g === hexo generate
hexo s === hexo server
hexo d === hexo deploy
```

更多命令您可以访问Hexo的官网：[Hexo](https://hexo.io/zh-cn/docs/commands.html "Hexo")

# 上传到github

现在只是在本地有了效果，接下来我们把本地的博客上传到github上。

## 创建仓库

注册帐号在这里略过。

应该注意的是，需要在github上先创建一个仓库，**命名为 yourusername.github.io** 。

## 全局声明

在Git Bash中声明自己的身份，输入以下命令：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

此处的 user.name 和 user.email 是github的账户名和登录邮箱。 * 注意是**账户名**而不是昵称 *

## 更改站点配置文件，后缀.yml

注意此处的**站点配置文件**是根目录下的.yml文件，而主题文件夹中的.yml文件是**主题配置文件**。

找到站点配置文件中的 deploy ，做如下更改：

```
deploy:
  type: git
  repo: git@github.com:username/username.github.io.git
  branch: master
```

# Hexo部署

```
$ hexo g
$ hexo d
```

此处步骤虽然简单，但是极易出问题。如果部署失败，请直接进行下一步。

# ssh配置

## 查看ssh

在Git Bash中输入 `ls -al ~/.ssh` ，查看是否生成过ssh，如果有就将Administrator文件夹（*即hexo文件夹的父级文件夹*）中的.ssh文件夹删除。

然后依次输入以下命令：

```
ssh-keygen -t rsa -C "example@xxx.com"     #邮箱为github的登录邮箱  
ssh-agent -s
ssh-add ~/.ssh/id_rsa
```

如果成功则进行下一步，如果出错显示 `Could not open a connection to your authentication agent` ，就输入以下命令：

```
eval `ssh-agent -s`
ssh-add
```

接下里就可以把key添加到github上了。输入命令复制key：

```
clip < ~/.ssh/id_rsa.pub
```

## 设置ssh

打开github，点击头像下拉菜单中的 setting 。然后在侧边栏找到 SSH and GPG keys ，点击绿色按钮 New SSH key , title 随便写一个，在key中粘贴刚才复制的 key ，点击 Add SSH key 。

然后在Git Bash中输入以下命令：

```
ssh -T git@github.com
```

你也许会看到有警告，输入“yes”继续。


输出

```
Hi username! You've successfully authenticated, but Github does not provide shell access.
```

就表示配置成功啦！

# 继续部署

```
$ hexo clean
$ hexo g
$ hexo d
```

看到 `Deploy done` 就表明部署成功了。接着在地址栏输入 https://username.github.io 就可以看到自己的博客啦。

现在，全世界都可以访问到你的站点。
