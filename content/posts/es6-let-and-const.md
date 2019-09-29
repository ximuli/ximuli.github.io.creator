---
title: ES6 系列：let 和 const
date: 2018-08-23
categories:
- 技术
tags: 
- JavaScript
---



# let 和 const



## let

> 我们不应该再使用 var 关键字。

let 的出现是为了方便地使用局部变量。

使用 var 关键词会有变量声明提升，let 则不会。

```javascript
{
    let a = 1;
    window.jewel = function() {
        console.log(a)
    }
}

console.log(a)  // Uncaught ReferenceError: a is not defined
```

let 的作用域只管到花括号。

```javascript
{
    let a = 1
}
console.log(a)  // Uncaught ReferenceError: a is not defined
```

let 可以嵌套。会出现「临时死区」（Temp  Dead Zone），如果在声明语句之前使用变量就会报错。

> JS 终于想通了，一个变量应该先声明再使用。

例如下面代码，如果在 let 声明之前使用 a 就会报错。



```javascript
{
    let a =1
    console.log(a)
    {
        let a = 2
        console.log(a)
        {
            let a = 3
            console.log(a)
        }
    }
}
```

let 不能重复声明。如下错误语法示例：

```javascript
{
    let a = 1
    let a = 2
}
```



## const

常量，给值之后就不要再改了。

const 只有一次赋值机会，而且必须在声明的时候马上赋值。

const 作用域也是止于花括号。

```javascript
{
    const PI = 3.1415926
    PI = 2
}

// Uncaught TypeError: Assignment to constant variable.
```



## 小结

1. let 的作用域在最近的 {} 之间
2. 如果在 let a 之前使用 a ，那么报错
3. 如果你重复（在同一作用域） let a ，那么报错

const 

1 2 3 同上

4. 只有一次赋值机会，而且必须在声明的时候马上赋值。



## 一个面试题

![image](http://wx4.sinaimg.cn/mw690/d1b5fd6bly1fujgtngc0cj20rz08mwej.jpg)

这样的代码我写过好多次，这就相当于刻舟求剑。点击的时候循环早运行完了。

怎样才能让结果符合预期呢？

有了 let 之后，这样的问题很好解决。

![image](http://wx1.sinaimg.cn/mw690/d1b5fd6bly1fujgtrreu7j20s408hjrg.jpg)

这是为什么？

因为 let 声明的 j 作用域就只在最近的 {} 中，每一次循环都会有一个对应的 j 。

如果我智障地非要不使用 let 呢？说白了，我们就是需要一个局部变量。那么在 ES 6 之前，局部变量一般都是怎么搞的？

立即执行函数。

![image](http://wx1.sinaimg.cn/mw690/d1b5fd6bly1fujgtuw4wmj20sa08vaa5.jpg)

当然， ES 6 中还有魔法。下面这种写法结果也是正确的：

![image](http://wx1.sinaimg.cn/mw690/d1b5fd6bly1fujgtyqnxsj20p10770th.jpg)



资料：

ES 6 新特性一览：https://frankfang.github.io/es-6-tutorials/

教程： es6.ruanyifeng.com



（完）








