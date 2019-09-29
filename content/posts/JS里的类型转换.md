---
title: JavaScript里的类型转换
date: 2018-05-17
categories: 
- 技术
tags: 
- JavaScript
---

# JS里的类型转换

## 任意类型转字符串

1. `xxx.toString()`

```javascript
(1).toString()  
// "1"
true.toString()  
// "true"
null.toString()
// Uncaught TypeError: Cannot read property 'toString' of null
undefined.toString()
// Uncaught TypeError: Cannot read property 'toString' of undefined
{}.toString()
// Uncaught SyntaxError: Unexpected token .
({}).toString()
// "[object Object]"
```

2. `String(xxx)`

```javascript
String(1)
// "1"
String(true)
// "true"
String(null)
// "null"
String(undefined)
// "undefined"
String({})
// "[object Object]"
```

3. `xxx + ''`，当然这种方法更简便

```javascript
1 + ''
// "1"
true + ''
// "true"
null + ''
// "null"
undefined + ''
// "undefined"
{} + ''
// 0
var obj = {}
obj + ''
// "[object Object]"
```



## 任意类型转布尔

1. `Boolean(xxx)`
2. `!!xxx`，老司机专用手法

```javascript
!!null
// false
!!undefined
// false
```

3. 5个 falsy 值

```javascript
0
NaN
''
null
undefined
```



## 任意类型转数字

1. `Number(xxx)`
2. `parseInt(xxx, 10)`
3. `parseFloat(xxx)`
4. `xxx - 0`
5. `+ xxx`



## 内存图

来看几道题目：

```javascript
var a = 1
var b = a
b = 2
//请问 a 显示是几？  


var a = {name: 'a'}
var b = a
b = {name: 'b'}
//请问现在 a.name 是多少？


var a = {name: 'a'}
var b = a
b.name = 'b'
//请问现在 a.name 是多少？


var a = {name: 'a'}
var b = a
b = null
//请问现在 a 是什么？
```



注：每当遇到这种问题，就老实地**画一下内存图**，把栈内存（Stack）和堆内存（Heap）都画出来，结果就会一目了然了。

* 简单类型的数据直接存在 Stack 里
* 复杂类型的数据是把 Heap 地址存在 Stack 里

另外，我在[《JavaScript高级程序设计》4.1.3--传递参数](http://blog.guozisha.com/%E3%80%8AJavaScript%E9%AB%98%E7%BA%A7%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E3%80%8B4-1-3-%E4%BC%A0%E9%80%92%E5%8F%82%E6%95%B0/) 一文中也解释过类似的问题，可以结合着看。



再来看一道题：

```javascript
var a = {n:1}
var b = a
a.x = a = {n:2}

alert(a.x)  //undefined
alert(b.x)  //[object Object]  
```

注意画图来理清思路。



## 关于循环引用

错误的例子：

```javascript
var a = {self: a}
a.self  //undefined
```

因为在赋值操作进行之前， 对象里 a 的值还是未声明的状态，值为 undefined



正确的写法：

```javascript
var a = {}
a.self = a
a.self  
//你可以一直 a.self.self.self 下去
```



## 垃圾回收

GC 垃圾回收 

如果一个对象没有被引用，它就是垃圾，将被回收。

来看一下简单的题目：

```javascript
var fn = function() {}
document.body.onclick = fn
fn = null
//请问例子中的函数现在是不是属于垃圾
```



![内存图](../imgs/内存图.jpg)



IE6有BUG内存泄露，关掉当前页面，并不会把document引用的对象视为垃圾，除非整个浏览器关闭。

解决方法也是有的，就是手动设置一下

```javascript
window.onunload=function (){document.body.onclick=null}
```



## 深拷贝和浅拷贝

* 基本类型赋值都是深拷贝，即拷贝后两者的值不互相影响

```javascript
var a = 1
var b = a
b = 2
a // 1
b // 2
```

* 复杂类型，对象的赋值就属于浅拷贝

```javascript
var a = {name: 'Jonathan'}
b = a
b.name = 'Jack'
a.name // 'Jack'
```



（完）



