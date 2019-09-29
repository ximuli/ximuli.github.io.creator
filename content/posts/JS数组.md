---
title: JS数组
date: 2018-05-29
categories: 
- 技术
tags: 
- JavaScript
---



# 标准库

> Number String Boolean 不加new 返回一个基本类型的值，加new返回复杂类型(对象)
>
> Object Array Function 加new不加new都一样，是返回复杂类型(对象)



![加new和不加的区别](../imgs/加new和不加的区别.jpg)




## 数组的本质

> 人类理解：数组就是数据的有序集合
> JS理解：数据就是原型链中有 Array.prototype 的对象

![数组的本质](../imgs/数组的本质.jpg)



## 伪数组

1. 有 0,1,2,3,4,5...n,length 这些 key 的对象
2. 原型链中没有 Array.prototype

这样的对象就是伪数组

目前知道的伪数组有：

1. arguments 对象
2. document.querySelectAll('div') 返回的对象




## 数组的 forEach()

自己实现一个简单的 forEach 函数：

```javascript
function forEach(arr, fn) {
    for(let i = 0; i < arr.length; i++) {
        fn(arr[i],i)
    }
}
forEach(['a','b','c'],function(value,key) {console.log(value,key)})
```

来看另一种方法：

```javascript
var obj = {0:'a',1:'b', length: 2}
obj.forEach = function(fn) {
  for (let i = 0; i<this.length; i++) {
    fn(this[i],i)
  }
}
obj.forEach(function (value,key) {console.log(value,key)})
//a 0
//b 1
```



## 数组的 sort()

* sort() 接收一个比较函数，比较函数接收两个参数

```javascript
var arr = [1,3,5,4,2]
arr.sort(function(a,b) {
  return a-b
})
//[1, 2, 3, 4, 5]
arr.sort(function(a,b) {
  return b-a
})
//[5, 4, 3, 2, 1]
```

* 数组相关的 API 里只有 sort() 会改变原数组




## 数组的 reduce()

* 接收一个函数和一个可选参数表示初始值

```javascript
var a = [1,2,3]
a.reduce(function(x,y) {
  return x+y
} ,0)
//6
```

更多请戳：[Array.prototype.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

* reduce() 是很强大的；来，把你绕晕：

```javascript
//map 可以用 reduce 来表示
var arr = [1,2,3]
a.reduce(function(arr, n) {
  arr.push(n*2)
  return arr
}, [])
//[2, 4, 6]

//filter 可以用 reduce 来表示
var a = [1,2,3,4,5,6,7,8,9,10]
a.reduce(function(arr, n) {
  if(n%2 === 0) {
    arr.push(n)
  }
  return arr
}, [])
//[2, 4, 6, 8, 10]
```



## 一道和数组有关的题目

```javascript
var a = [1,2,3,4,5,6,7,8,9]
a.reduce(???,???)
//计算所有奇数的和
a.reduce(function(num,x) {
    if (x%2 !== 0) {
        num += x
    }
    return num
}, 0)
//25
```



参考资料：

[标准库--JavaScript标准参考教程](http://javascript.ruanyifeng.com/#toc2)



（完）