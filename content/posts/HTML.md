---
title: HTML 温故而知新 
date: 2018-04-15
categories: 
- 技术
tags: 
- HTML
---

> 先搞清楚要做什么，做的过程中需要学什么就去学什么。先用再学才是学编程 的不二法门。

# HTML

HpyerText Markup Language



## W3C

万维网联盟（World Wide Web Consortium），又称 W3C 理事会，是万维网的主要国际标准组织。由蒂姆·伯纳斯-李于1994年10月离开欧洲核子研究中心（CERN）后成立。

W3C 根据浏览器的实际情况总结文档，并不是凭空想象。

W3C制定的网络标准并非强制而只是推荐标准。



## MDN

MDN Web Docs（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网络技术开发文档的免费网站。



## 关于标签

* 理解清楚每个标签的含义，关注标签语义化；不要老用 `div` ，`div` 是没有任何语义的



* HTML5 的 DOCTYPE 是 `<!DOCTYPE html>` ，其他版本都很难记。当然也可以做一些了解：

  [https://www.w3.org/QA/2002/04/valid-dtd-list.html](https://www.w3.org/QA/2002/04/valid-dtd-list.html)

* `html` `head` `body` 这些标签实际上在特定情况下是可以省略的，我们可以查看文档*（搜索 HTML spec）* 来了解：https://www.w3.org/TR/html5/    当然，如果你嫌弃文档，也可以直接在 MDN 上搜索

* 常见的一些标签：a、form、input、button、h1、p、ul、ol、small、strong、div、span、kbd、video、audio、svg 。基本上了解标签对应单词的意思，就知道这个标签怎么用了。（关注语义化）





## 空元素

一个**[空元素（empty element）](https://developer.mozilla.org/zh-CN/docs/Glossary/%E7%A9%BA%E5%85%83%E7%B4%A0)**可能是 HTML，SVG，或者 MathML 里的一个**不可能存在子节点** （例如内嵌的元素或者元素内的文本）的 element 。

在 HTML 中，通常在一个空元素上使用一个闭标签是无效的。

例如， `<input type="text"> </input>` 的闭标签是无效的 HTML。

HTML 有以下这些空元素：

* `<area>`
* `<base>`
* `<br>`
* `<col>`
* `<colgroup>`  when the `span` is present 
* `<command>`
* `<embed>`
* `<hr>`
* `<img>`
* `<input>`
* `<keygen>`
* `<link>`
* `<meta>`
* `<param>`
* `<source>`
* `<track>`
* `<wbr>`





## 可替换元素

CSS 里，**可替换元素（replaced element）**的展现不是由CSS来控制的。这些元素是一类 外观渲染独立于CSS的 外部对象。

典型的可替换元素有 `<img>` `<object>` `<video>` 和表单元素，如 `<textarea>` `<input>` 。某些元素只在一些特殊情况下表现为可替换元素，例如 `<audio>` 和 `<canvas>` 。通过 CSS `content` 属性来插入的对象被称作 匿名可替换元素。

以上是 MDN 里对 可替换元素 的解释。可以看到，这样的解释还是相当抽象的，我依然不是很明白，于是又查了一下相关的内容，发现写这个内容的博客还不少。



总结如下：

没有实际内容，浏览器根据其标签的元素与属性来判断显示具体的内容。

> 例如浏览器会根据标签的`src`属性的值来读取图片信息并显示出来，而如果查看`html`代码，则看不到图片的实际内容；又例如根据标签的`type`属性来决定是显示输入框，还是单选按钮等。



学习资料：

[HEAD -- A list of everything that *could* go in the `<head>` of your document](https://github.com/joshbuchea/HEAD)

[HTML(超文本标记语言) | MDN](http://www.baidu.com/link?url=Vnxb80o3GUeDZ89yKoI5s_KIzAys6X_02nBV9KKjWd35IlNtVgf2ZANGTH127t963hStQQGB6l60-y-9sgx40K)

[HTML 测验](http://www.w3school.com.cn/quiz/quiz.asp?quiz=html)

[W3Schools HTML Quiz](https://www.w3schools.com/quiztest/quiztest.asp?qtest=HTML)

[Dribbble.com](https://dribbble.com/)



一些小知识：

1. `a` 标签的英文全称： anchor
2. noscript 标签：如果用户浏览器不支持 script ，则会显示 noscript 中的内容
3. 命令行 `whois`
4. 关于 `iframe` 
   * iframe 用于在当前页面里嵌入一个页面
   * iframe 可以拥有一个 name，a 标签的 target 可以通过 name 指向这个 iframe
   * 现代前端开发中，iframe 很少用
5. 声明当前页面 charset 
   *  `<meta charset="utf-8">`
   *  `<meta http-equiv="content-type" content="text/html; charset=utf-8" >`



（完）

