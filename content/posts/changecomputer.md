---
title: 换电脑后如何在新电脑上更新博客
date: 2017-02-23 17:07
categories:
- 技术
tags: 
- Hexo
- Github
---

最近换用了小姐姐的笔记本电脑，用起来比我原来的破电脑流畅多了。

<!-- more -->

其实我比较菜，在知乎上查换电脑如何更新Hexo博客，查到教人怎么做博客的，直到最近把电脑的各种软件安装好，搬着我的小梯子翻了半天，才找到一点有用的线索。在这之前我已经把整个博客的hexo文件夹复制打包放优盘里带到了上海……

*正文开始：* 

首先当然是安装好Git和Node.js，打开Git Bash把`npm`源改成淘宝的`cnpm` ，然后安装Hexo

```
cnpm install -g hexo
```

然后把我辛苦打包的hexo文件夹解压出来，进入目录。（自行选择放到哪个盘里）

在hexo目录下打开Git Bash，就可以开始输入Hexo的命令了：

```
hexo clean
hexo g
hexo s
```

在之前的文章中我们配置过ssh，那么现在应该重新换一个了吧，参考原文章就可以，[《Hexo 踩坑笔记：利用Hexo和github pages服务搭建个人博客》](http://blog.learnerdaily.com/test/) ，接下来就可以放心部署啦

```
hexo d
```

然而我部署的时候报错了：

```
not a git repository (or any of the parent directories): .git   
......
```

直接把hexo目录下的 .deploy_git 文件夹删除，之后再重新部署，就没有问题啦。

好像并没有什么难度哈，谁让我傻到把hexo文件夹全部复制打包了呢……