---
title: CSS 温故而知新
date: 2018-04-30
categories: 
- 技术
tags: 
- CSS
---



> 中文学习资源只看大 V 的（毕竟他们要维护形象不能瞎写），英文资源看 CSS Tricks、MDN 和 Codrops。书的话作用不大，最权威的书其实是文档。
>
> 如果你想快速上手，就先写小 demo 再学理论。
>
> 如果你想一鸣惊人，就仔细看 CSS 规范文档。
>
> 查询CSS文档请直接搜索 CSS spec



# 知识点

## 引入CSS的四种方式

style 属性、style 标签、css link、css import



## 高度由什么决定

> div 高度由其内部文档流元素的高度总和决定。



### 文档流

问：什么是文档流？

答：文档内元素的流动方向。



#### 需要关注的几点：

* 内联元素从左向右流动，如果容器宽度不够，就换行继续从左向右流动
* 块元素独占一行，依次从上往下流
* 如果一个内联元素中有一个很长的单词，那么容器宽度不够时默认是不会分成两段显示的。因为浏览器认为这个单词是一个整体。 CSS 中 `word-break` 属性可以控制这种情况。




#### 内联元素的高度由什么决定？

* 无力吐槽 o(╥﹏╥)o
* `line-height`


* 与字体和字体设计师设置的一些参数有关。




参考：[深入理解 CSS：字体度量、line-height 和 vertical-align](https://zhuanlan.zhihu.com/p/25808995?group_id=825729887779307520)



# 布局与居中

## 左右横向布局

float + clearfix

给所有子元素添加 float ，给其父元素添加 clearfix 。

```css
.clearfix:after {
  content: "";
  display: block;
  clear: both;
} 
```

注：此方法同样适用于左中右布局。



## div 水平居中

```css
margin-left: auto;
margin-right: auto;
```



## 垂直居中

`line-height`

div高度为 30px，div 里有一行字垂直居中，字的大小为 14px：

- 给div的样式为 `font-size：14px；line-height：20px; padding: 5px 0;`
- 给div的样式为 `font-size：14px；line-height：24px; padding: 3px 0;`
- 给div的样式为 `font-size: 14px;  line-height: 30px;`



注：

* css 布局想要 BUG 少，尽量不要写 `width` 和 `height` 。
* `max-width` 比 `width` 更好用一点。
* `display：inline-block` 一定要加 `vertical-align:top` 。
* `::before` `::after` 是伪元素，必须给 `content: '';` ；`:hover` `:nth-child()` 是伪类。




# CSS 学习资源

1. Google: 关键词 MDN
2. [CSS Tricks](https://css-tricks.com/)
3. [Google: 阮一峰 css](https://www.google.com/search?q=%E9%98%AE%E4%B8%80%E5%B3%B0+css)
4. [张鑫旭的 240 多篇 CSS 博客](http://www.zhangxinxu.com/wordpress/category/css/page/25/)
5. [Codrops 炫酷 CSS 效果](https://tympanus.net/codrops/category/playground/)
6. [CSS揭秘](http://www.ituring.com.cn/book/1695)
7. [CSS 2.1 中文 spec](http://cndevdocs.com/)
8. [Magic of CSS](http://adamschwartz.co/magic-of-css/) 免费在线书


（完）