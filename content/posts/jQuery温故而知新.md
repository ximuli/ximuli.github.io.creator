---
title: jQuery温故而知新
date: 2018-06-24
categories:
- 技术
tags: 
- JavaScript
---

>**jQuery** 是专注于简化 [DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM) 操作，[AJAX](https://developer.mozilla.org/en-US/docs/Glossary/AJAX) 调用和 [Event](https://developer.mozilla.org/en-US/docs/Glossary/Event) 处理的 [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) [库](https://developer.mozilla.org/zh-CN/docs/Glossary/%E5%BA%93)。它被 JavaScript 开发者频繁使用。
>
>jQuery 使用 `$(selector).action()` 的格式给一个（或多个）元素绑定事件。具体来说，`$(selector)` 调用 jQuery 函数选择 `selector` 元素，并给它绑定一个叫 `.action` 的事件 [API](https://developer.mozilla.org/en-US/docs/Glossary/API)。



# 自己封装两个函数

本文以下面这段 HTML 作为示例：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
<ul>
  <li id="item1">选项1</li>
  <li id="item2">选项2</li>
  <li id="item3">选项3</li>
  <li id="item4">选项4</li>
  <li id="item5">选项5</li>
</ul>
</body>
</html>
```



封装一个函数，获取到一个节点的所有兄弟姐妹

```javascript
function getSiblings(node) {}

function getSiblings(node) {
  var allChildren = node.parentNode.children;
  var arr = {length:0}
  for (let i = 0; i < allChildren.length; i++) {
    if (allChildren[i] !== node) {
      arr[arr.length] = allChildren[i]  
      //之所以不用 arr[i] 是因为可能会跳过，导致 arr 的 key 会不完整；
      //使用 arr[arr.length] 可以很好的给伪数组添加完整的数字 key 
      arr.length += 1
    }
  } 
  return arr
}
```



再封装一个，用来添加和删除 class

```javascript
function addClass(node, classes){}

function addClass(node,classes) {  //classes的写法例如：{'a':false,'b':false,'c':true}
  for (let key in classes) {
    var value = classes[key]
    if (value) {
      node.classList.add(key)
    }
    else {
      node.classList.remove(key)  // 一旦出现相同的代码，就存在优化的可能
    }
  }
}

// 看一下优化后的代码
function addClass(node,classes) { 
  for (let key in classes) {
    var value = classes[key]
    var methodName = value ? 'add' : 'remove'
    node.classList[methodName](key)
  }
}

```



# 命名空间

一种设计模式。一个著名的库就是这样用的，yui

```javascript
window.ffdom = {}
ffdom.getSiblings = getSiblings
ffdom.addClass = addClass

ffdom.getSiblings(node)
ffdom.addClass(node, classes)
```



# 能不能把 node 放在前面

```javascript
node.getSiblings()
node.addClass()
```

方法一：扩展 node 接口

直接在 Node.prototype 上加函数

```javascript
Node.prototype.getSiblings = function() {
  var allChildren = this.parentNode.children  //使用 this
  var arr = {length:0}
  for (let i = 0; i < allChildren.length; i++) {
    if (allChildren[i] !== this) {
      arr[arr.length] = allChildren[i] 
      arr.length += 1
    }
  } 
  return arr
}

Node.prototype.addClass = function(classes) {
    for (let key in classes) {
    var value = classes[key]
    var methodName = value ? 'add' : 'remove'
    this.classList[methodName](key)
  }
}

node.getSiblings()
node.addClass()
```

方法二：新的接口

```javascript
window.Node2 = function(node) {
    return {
        getSilings: function() {
          var allChildren = node.parentNode.children 
          var arr = {length:0}
          for (let i = 0; i < allChildren.length; i++) {
            if (allChildren[i] !== node) {
              arr[arr.length] = allChildren[i] 
              arr.length += 1
            }
          } 
          return arr
        },
        addClass: function(classes) {
          for (let key in classes) {
            var value = classes[key]
            var methodName = value ? 'add' : 'remove'
            node.classList[methodName](key)
          }
        }
    }
}

var node2 = Node2(node)
node2.getSilings()
node2.addClass()
```

我们可以把 Node2 写成 jQuery；除此之外，我们改写一下功能

```javascript
window.jQuery = function(nodeOrSelector) {
  let nodes = {}
  if (typeof nodeOrSelector === 'string') {
    let temp = document.querySelectorAll(nodeOrSelector)  //伪数组
    for (let i = 0; i < temp.length; i++) {  // 通过 for 循环来去掉一些多余的 key
      nodes[i] = temp[i]
    }
      nodes.length = temp.length
  }  
  else if (nodeOrSelector instanceof Node) {
    nodes = {0: nodeOrSelector,length: 1}
  }
  
  nodes.getSiblings = function() {}  //过于复杂先跳过
  nodes.addClass = function(classes) {
    classes.forEach((value) => {
      for (let i = 0; i < nodes.length; i++) {
        nodes[i].classList.add(value)      
      }      
    }) 
  }
  
  nodes.getText = function () {
    let texts = []
    for (let i = 0; i < nodes.length; i++) {
      texts.push(nodes[i].textContent)
    }
    return texts
  }
  nodes.setText = function (text) {
    for (let i = 0; i < nodes.length; i++) {
      nodes[i].textContent = text
    }
    return texts
  }
  
  //jQuery 非常讨厌使用 get 和 set ，经常会把这种操作合并，根据参数来决定 get 还是 set
  nodes.text = function (text) {
    if (text === undefined) {
      let texts = []
      for (let i = 0; i < nodes.length; i++) {
        texts.push(nodes[i].textContent)
      }
      return texts
    }
    else {
      for (let i = 0; i < nodes.length; i++) {
        nodes[i].textContent = text
      }
      return texts
    }
  }
  //在 jQuery 中随处可见类似的 API
  
  return nodes
  
}

var node2 = jQuery('ul li')
node2.addClass(['blue'])
```



# Source Map 

jQuery 官网提供了几种不同的版本，你是否知道这些版本有什么区别？

第一个地址是压缩后用于生产环境的版本，混淆版；

第二个地址是未压缩的开发版本，未混淆；

第三个地址是「 map file for jQuery 」，简单说，Source map就是一个信息文件，里面储存着位置信息。也就是说，转换后的代码的每一个位置，所对应的转换前的位置。

可以查看 [这篇文章](http://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html) 详细了解。 

![jQuery的版本](./../imgs/jQuery的版本.jpg)



# jQuery 和 DOM API 获取的元素有什么联系和区别？

jQuery 获取的元素组成 jQuery 对象，只可以执行 jQuery 的方法；DOM API 获取的元素是 DOM 对象，只可以执行 DOM 的方法。

```html
<div id=x></div>
```

```javascript
var div = document.getElementById('x')
var $div = $('#x')  // jQuery 对象
```

联系（相互转换）：

由 jQuery 对象转换为 DOM 对象，

```javascript
//1. jQuery 选择器返回的对象是伪数组，可以使用中括号来访问其中的某一项
$div[0]   // DOM 对象

//2. 使用 jQuery 提供的 get 方法
$div.get(0)  // DOM 对象
```

由 DOM 对象转换为 jQuery 对象，

```javascript
// 对于 DOM 对象，只需用 $() 把 DOM 对象包装起来，就可得到 jQuery 对象
$(div)  // jQuery 对象
```



学习资料：

[jQuery设计思想 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html)

[jQuery最佳实践 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2011/08/jquery_best_practices.html)

[为什么推荐使用 === 不推荐 ==](https://zhuanlan.zhihu.com/p/22745278)

（完）