---
title: DOM-API
date: 2018-06-10
categories:
- 技术
tags: 
- JavaScript
---

# 对 DOM 的理解

1. 文档对象模型：Document Object Model
2. D 在此表示 XML 文档，HTML 是 XML 的一种衍生品；O 表示 Object ，在内存中，通过构造函数（如 Document，Element，Text，Comment 等等）构造出对象；M 表示 Model，表示 Document 和 Object 映射关系的模型；所以称为 DOM
3. 页面中的节点 ===>  通过构造函数 ===> 对象，这就是 DOM 的主要功能



# Node

## 对 Node 的理解

1. Node 即节点，分为 Document，Element，Text 以及其他不重要的。
2. JS里的对象，都是继承自 Object 的；页面里的对象，都是继承自 Node，跟 NodeJS 没关系，这里的 Node 是一个函数，一般我们不会自己去用这个函数
3. Node 最终又是继承自 Object 的

```javascript
// 为了便于理解，我们可以在控制台打出节点，看一下它们的原型链上到底存在些什么东西
console.dir(document.body)
console.dir(document.documentElement)  //document.documentElement 返回文档对象的根元素
```

下面这张图一定可以帮助你更加理解 Node：

![Node的接口](../imgs/Node的接口.jpg)



## 属性

childNodes,firstChild,innerText,lastChild,nextSibling,nodeName,nodeType,nodeValue,outerText

ownerDocument,parentElement,parentNode,previousSibling,textContent

* Node.childNodes 是最特殊的，它返回的是一个伪数组，里面是Node节点，并且伪数组内的值是动态变化的；只有 Node.querySelectorAll() 返回的数组不是动态的


* nodeName 获取到的节点名称是大写的，只有一个特殊的 svg 是小写
* [innerText 和 textContent](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent)





## 方法

如果一个属性是函数，那么这个属性就也叫做方法；换言之，方法是函数属性

- appendChild()
- cloneNode()
- contains()
- hasChildNodes()
- insertBefore()
- isEqualNode()
- isSameNode()
- removeChild()
- replaceChild()
- normalize() // 常规化

1. 搞清楚英文单词的意思就知道用法
2. 如果发现知道英文后依然不明白用法，看 MDN 的例子即可，如 [normalize](https://developer.mozilla.org/en-US/docs/Web/API/Node/normalize)



DOM APi 无外乎「增删改查」

关于 Document 和 Element 的属性和方法不在此一一列举，请直接查看 MDN 文档学习。



## 题目

1. DOM 的最小组成单位叫做 Node （节点）
2. 节点的类型有七种，分别是？
3. DOM 树的根节点是？
4. 元素 Element 的NodeType 值为？
5. document.body.nodeName 返回什么？
6. HTMLCollection 与 NodeList 的区别有？




学习资料：

[Node - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Node)

[Document - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Document)

[Element - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)

[DOM模型 - JavaScript 标准参考教程 ](http://javascript.ruanyifeng.com/#toc5)



参考博客：

[DOM 结构](https://github.com/wojiaofengzhongzhuifeng/myBlog/issues/19)

（完）
