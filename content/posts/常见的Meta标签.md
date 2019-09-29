---
title: 常用Meta标签用法记录
date: 2017-02-07
categories:
- 技术
tags: 
- HTML
---

# `<meta>` 常用标签全记录

*平常见到某些网站头部的`<meta>`标签有一大串，然而我并不知道其具体作用都是什么，现做如下整理，便于以后开发中的使用。* 

<!-- more -->

`<meta>` 元素可提供有关某个 HTML 元素的元信息 (meta-information)，比如描述、针对搜索引擎的关键词以及刷新频率。

meta标签的可选属性有两个，分别是：`name`和`http-equiv`，必要属性为`content`。

> meta常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。

## name属性

### renderer

作用于双核浏览器

```
<meta name="renderer" content="webkit">                  //让双核浏览器使用webkit内核渲染页面
<meta name="renderer" content="ie-comp">                 //默认IE兼容模式
<meta name="renderer" content="ie-stand">                //默认IE标准模式
```

### UC和QQ

```
<meta name="screen-orientation" content="portrait">      //UC强制竖屏；
<meta name="x5-orientation" content="portrait">          //QQ强制竖屏；
<meta name="full-screen" content="yes">                  //UC强制全屏；
<meta name="x5-fullscreen" content="true">               //QQ强制全屏
<meta name="browsermode" content="application">          //UC应用模式
<meta name="x5-page-mode" content="app">                 //QQ应用模式;
```

### robots

```
<meta name="robots"content="none">
```

robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。content的参数有all,none,index,noindex,follow,nofollow。默认是all。

1. 信息参数为all：文件将被检索，且页面上的链接可以被查询；
2. 信息参数为none：文件将不被检索，且页面上的链接不可以被查询；
3. 信息参数为index：文件将被检索；
4. 信息参数为follow：页面上的链接可以被查询；
5. 信息参数为noindex：文件将不被检索，但页面上的链接可以被查询；
6. 信息参数为nofollow：文件将被检索，但页面上的链接不可以被查询。

### viewport

常用于移动端的设计中。

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### copyright版权

```
<meta name="copyright"content="Jonathan"> 
```

###  revisit-after

用于设置搜索引擎爬虫的重访时间。为了减轻搜索引擎爬虫对服务器带来的压力，可以设置此值。

```
<meta name="revisit-after" content="10 days" >
```



## http-equiv属性

### X-UA-Compatible

用于告知浏览器应以何种版本来渲染页面

```
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">   //指定IE和Chrome使用最新版本渲染当前页面
```

### content-Type

用于设定网页字符集

```
<meta charset="utf-8">    // HTML5
<meta http-equiv="content-Type" content="text/html;charset=uft-8">
```

### cache-control

```
<meta http-equiv="Cache-Control" content="no-transform">  //禁止自动转码
<meta http-equiv="cache-control" content="no-siteapp">    //禁止自动转码
<meta http-equiv="pragma" content="no-cache">             //禁止浏览器从本地计算机的缓存中访问页面内容
<meta http-equiv="cache-control" content="no-cache">      //禁止缓存
```



*我将继续查看各大网站的`<meta>`标签并搜索相关用法，本文持续更新……* 