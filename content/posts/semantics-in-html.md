---
title: HTML语义化
date: 2019-03-06 21:39:32
categories:
- interview
---

简单来说，我们可以理解为：用正确的标签做正确的事情。

例如：

段落用 p 标签，标题用 h 系列标签，边栏用 aside 标签，主要内容用 main 标签。

**正确使用语义标签可以带来很多好处。**

<!-- more -->

# 为什么要关注 HTML 语义化？（为什么要使用语义类标签？）

对人：

- 增强可读性，对开发者更友好，在没有 CSS 的情况下也能较好地呈现网页的内容结构与代码结构，便于团队的开发和维护。

对机器：

- 有利于 SEO ，可以让搜索引擎爬虫更好地获取到更多有效信息，搜索引擎的爬虫依赖于标签来确定上下文和各个关键字的权重，有效提升网页的搜索量。
- 支持读屏软件，方便其他设备的解析（如屏幕阅读器、盲人阅读器等），利于无障碍阅读，提高可访问性。

# 一些语义类标签介绍

`<header>`

用于展示介绍性内容，通常包含一组介绍性的或是辅助导航的实用元素。

`<footer>`

表示最近一个章节内容或者根节点元素的页脚。通常出现在尾部，包含一些作者信息、相关链接、版权信息等。

`<aside>`

表示跟文章主体不那么相关的部分，可能包含导航、广告等工具性质的内容。

侧边栏是 aside，aside 不一定是侧边栏。

aside 和 header 中都可能出现导航 `<nav> `，header 中的导航多数是到文章的目录，而 aside 中的导航多是到关联页面或者整站地图。

`<address>`

footer 中可以包含此元素。

容易误用，并非表示单纯的地址，而是表示「文章作者的联系方式」。

> 可以让作者为它最近的 `<article>` 或者 `<body>` 祖先元素提供联系信息。在后一种情况下，它应用于整个文档。

`<hgroup>`

表示标题组。

`<em>` 

表示重音。同样一句话里如果重音不同，表达的意思也许大相径庭。

`<strong>`

表示文本十分重要，一般用粗体显示。

`<abbr>`

表示缩写。

`<hr>`

横向分割线，表示段落级元素之间的主题转换（例如，一个故事中的场景的改变，或一个章节的主题的改变）。

`<blockqoute>`

表示段落级引述内容。

`<q>`

表示行内的引述内容。

`<cite>`

表示引述的作品名。

`<time>`

表示24小时制时间。

`<figure>` 和 `<figcaption>`

两者常配合使用，表示一段独立的内容，并且作为一个独立的引用单元。

> 当它属于主体(main flow)时，它的位置独立于主体。这个标签经常是在主文中引用的图片，插图，表格，代码段等等，当这部分转移到附录中或者其他页面时不会影响到主体。 -- MDN

```html
<figure>
  <img src="https://xx.com/xx.png" alt="An awesome picture">	
  <figcaption>这是一张图片。</figcaption>
</figure>
```

`<dfn>`

表示术语的一个定义。

```html
<p>
    <dfn id="def-internet">The Internet</dfn> is a global system of interconnected networks that use the Internet Protocol Suite (TCP/IP) to serve billions of users worldwide.
</p>
```

`<nav>` `<ol>` `<ul>`

导航栏、有序列表、无序列表

`<pre>` 中的内容会保持原有格式。

`<samp>` 元素用于标识计算机程序输出。

`<code>` 表示一段计算机代码。


# 总结

对于语义类标签的使用也许会带来一些争议，我们应该遵循的原则是：

> 尽量只用自己熟悉的语义标签。
>
> 用对比不用好，不用比用错好。


提示：

你可以在百度或者谷歌搜索中输入「标签名称」+「MDN」这两个关键字来查看更加专业和详细的解释。


另外安利一个 HTML 标签的学习链接：

[HTML Reference - A free guide to all HTML elements and attributes](https://htmlreference.io/)


（完）