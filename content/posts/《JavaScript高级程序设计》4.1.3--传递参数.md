---
title: 《JavaScript高级程序设计》4.1.3--传递参数
date: 2018-01-10
categories: 
- 技术
tags: 
- JavaScript
---

# 章节 4.1.3 ——传递参数

> page：70

ECMAScript 中所有函数的参数都是**按值传递**的。（这里之所以这样写，是因为某些编程语言在传递参数的时候，既可以选择按值传递，也可以选择按引用传递，例如PHP。）

然而在JavaScript当中，参数只能按值传递。一个经典的例子如下：

```javascript
function setName(obj) {
  obj.name = 'Jonathan';
}
var person = new Object();
setName(person);
alert(person.name);    //'Jonathan'
```

看起来很正常。

我自己的臆想中把 person 传到函数中是这样的：

```javascript
function setName(person) {
  person.name = 'Jonathan'; 
}
```

但是其中的实现方式并非如此。

实际的情况应该是这样的：

  ![传递参数1](..\imgs\传递参数1.jpg)

当变量 person 被当做参数传入函数中时，就被复制给了变量 obj，在这时 obj 和 person 指向的是同一个对象，所以当 `obj.name = "Jonathan"`时，函数外部 person 的 name 属性也会变为 Jonathan。

再来看另一个例子：

```javascript
function setName(obj) {
  obj.name = 'Jonathan';
  obj = new Object();
  obj.name = '胡歌';
}
var person = new Object();
setName(person);
alert(person.name);    //'Jonathan'
```

刚开始的时候我确实很困惑，为什么 person 的值没有变化，但是用图来表示的话，就清楚很多了：

  ![传递参数2](..\imgs\传递参数2.jpg)

在 setName 函数中一个新对象被赋值给变量 obj ，也就改变了其指向，所以此时无论对 obj 做任何操作，和变量 person 指向的对象都没有任何关系。

> 实际上，当在函数内部重写 obj 时，这个变量的引用就是一个局部对象了。而这个局部对象会在函数执行完毕后立即被销毁。