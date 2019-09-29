---
title: JS函数
date: 2018-06-01
categories:
- 技术
tags: 
- JavaScript
---

# 函数的五种声明方式

1. 具名函数

```javascript
 function f(x,y){
     return x+y
 }
 f.name // 'f'
```

2. 匿名函数

```javascript
var f
 f = function(x,y){
     return x+y
 }
 f.name // 'f'
```

3. 具名函数赋值

```javascript
 var f
 f = function f2(x,y){ return x+y }
 f.name // 'f2'
 console.log(f2) // Uncaught ReferenceError: f2 is not defined
```

4. window.Function  （不推荐）

```javascript
 var f = new Function('x','y','return x+y')
 f.name // "anonymous"
```

5. 箭头函数

```javascript
 var f = (x,y) => {
     return x+y
 }
 
 var sum = (x,y) => x+y
 //等同于
 var sum = (x,y) => {return x+y}
  
 var n2 = n => n*n
 //等同于
 var n2 = (n) => {return n*n}
```



> 注意函数的 name 属性在不同的声明方法中各种不同的表现。



# 函数的本质

> 函数就是一段可以反复调用的代码块。

1. 回顾一下

![回顾原型](../imgs/回顾原型.jpg)



2. 函数的调用

>
>f.call(asThis, input1,input2)
>其中 asThis 会被当做 this，[input1,input2] 会被当做 arguments
>禁止使用 f(input1, input2)，因为学会 .call 才能理解 this
>

![函数的本质](../imgs/函数的本质.jpg)



# this 和 arguments

![this-arguments](../imgs/this-arguments.jpg)

来看一个例子：

```javascript
var f = function () {
  console.log(this)
  console.log(this === window)
}

f.call(undefined,2,3)
// Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, frames: Window, …}
// true
```

第一个参数明明是 undefined，但是浏览器自动把 this 变成了 window。

我们需要用严格模式来看一下：

```javascript
var f = function () {
  'use strict'
  console.log(this)
  console.log(this === window)
}

f.call(undefined,2,3)
// undefined
// false

f.call('666',3,4)
// 666
// false
```

这样才符合我们的预期，即：this 就是 call 中的第一个参数；而后面的参数则组成 arguments 。




# call stack

* call stack（调用堆栈）先入后出
* 每进入一个函数中，会把函数的位置记录在 stack 里面，等 return 的时候就回到 stack 最顶部的位置。

递归，每次进一个函数就要压一次 stack，压入过多会导致 stack overflow

```javascript
function sum(n) {
  if (n === 1) {
    return 1
  }
  else {
    return n + sum.call(undefined, n-1)
  }
}
sum.call(undefined, 5)//试着把这个值改成很大的值，会出现 stack overflow
//15
sum.call(undefined, 27988)  // 2018年6月1日 Chrome
//391678066
sum.call(undefined, 27989)
//Uncaught RangeError: Maximum call stack size exceeded
```

来看几个可视化的例子：


- [普通调用](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gYSgpewogICAgY29uc29sZS5sb2coJ2EnKQogIHJldHVybiAnYScgIAp9CgpmdW5jdGlvbiBiKCl7CiAgICBjb25zb2xlLmxvZygnYicpCiAgICByZXR1cm4gJ2InCn0KCmZ1bmN0aW9uIGMoKXsKICAgIGNvbnNvbGUubG9nKCdjJykKICAgIHJldHVybiAnYycKfQoKYS5jYWxsKCkKYi5jYWxsKCkKYy5jYWxsKCk%3D!!!)
- [嵌套调用](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gYSgpewogICAgY29uc29sZS5sb2coJ2ExJykKICAgIGIuY2FsbCgpCiAgICBjb25zb2xlLmxvZygnYTInKQogIHJldHVybiAnYScgIAp9CmZ1bmN0aW9uIGIoKXsKICAgIGNvbnNvbGUubG9nKCdiMScpCiAgICBjLmNhbGwoKQogICAgY29uc29sZS5sb2coJ2IyJykKICAgIHJldHVybiAnYicKfQpmdW5jdGlvbiBjKCl7CiAgICBjb25zb2xlLmxvZygnYycpCiAgICByZXR1cm4gJ2MnCn0KYS5jYWxsKCkKY29uc29sZS5sb2coJ2VuZCcp!!!)
- [递归调用](http://latentflip.com/loupe/?code=ZnVuY3Rpb24gc3VtKG4pewogICAgaWYobj09MSl7CiAgICAgICAgcmV0dXJuIDEKICAgIH1lbHNlewogICAgICAgIHJldHVybiBuICsgc3VtLmNhbGwodW5kZWZpbmVkLCBuLTEpCiAgICB9Cn0KCnN1bS5jYWxsKHVuZGVmaW5lZCw1KQ%3D%3D!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)





# 作用域

* 变量声明提升

```javascript
var a = 1
function f1(){
    alert(a) // 是多少
    var a = 2
}
f1.call()
```



* 就近原则

```javascript
var a = 1
function f1(){
    var a = 2
    f2.call()
}
function f2(){
    console.log(a) // 是多少
}
f1.call()
```



* 我们只能确定变量是哪个变量，但是不能确定变量的值

```javascript
// 先来写 6 个 li 标签
var liTags = document.querySelectorAll('li')
for(var i = 0; i<liTags.length; i++){
    liTags[i].onclick = function(){
        console.log(i) // 点击第3个 li 时，打印 2 还是打印 6？
    }
}
```



# 闭包

> 如果一个函数，使用了它范围外的变量，那么（这个函数 + 这个变量）就叫做闭包。



请参看：

[JS 中的闭包是什么？](https://zhuanlan.zhihu.com/p/22486908)



（待续）