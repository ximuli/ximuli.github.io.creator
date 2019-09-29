---
title: FCC之路：Seek and Destroy（摧毁数组）
date: 2017-08-27
categories: 
  - 技术
tags: 
  - JavaScript
---

>实现一个摧毁(destroyer)函数，第一个参数是待摧毁的数组，其余的参数是待摧毁的值。
>例子： destroyer([1, 2, 3, 1, 2, 3], 2, 3) 应该返回 [1, 1].



*一些简单的算法题我总是能卡好久，之所以说简单，是因为苦苦思考无结果后到网上找答案，经常是随便几行代码就行搞定。然而这些网上的答案很多都是写一堆废话，然后粘几行没有注释的代码，看起来颇为吃力，根本不知道该怎么理解。暂且做个记录。*

<!-- more -->

# 解法1

```
function destroyer(arr) {
  // Remove all the values
  var arr_arg = arguments;    // 提前获取destroyer函数的arguments对象
  for(var i = 1; i < arr_arg.length; i++){
    arr = arr.filter(function(val){
      return arr_arg[i] !== val;    // 其他倒还好，就是不理解这行的意思
    });
    }
  return arr;
}
destroyer([1, 2, 3, 1, 2, 3], 2, 3);
```

我好像明白了一点，先来看一段MDN上关于filter()方法的描述：
>filter 为数组中的**每个元素调用一次 callback函数**，并利用所有使得 callback返回 true 或 等价于 true 的值的元素创建一个新数组。

其实解法1中就好像是一个双重的循环，在提前保存了destroyer函数的arguments对象之后，展开了一个除去 arguments 第一项之外的循环，即 i 值从1开始的循环。

而 filter 也相当于一个循环，其回调函数的参数 val 正是代表数组 arr 的值，然后 filter 把数组 arr 每一项的值都和 arr_arg[i] 作比较来决定返回 true 或者 false 。（如果按照这个说法，那函数destroyer的for循环在第一次循环的时候 val 应该是一个数组，即 [1, 2, 3, 1, 2, 3] , 但是我试着在回调函数的 return 之前加上了 alert(val) ，却依次弹出了1,2,3,1,2,3；还是不理解。）



# 解法2

```
function destroyer(arr) {
  var arr1 = [];
  for(var i = 1; i < arguments.length; i++){
    arr1.push(arguments[i]);
  }
  var arr2 = arr.filter(function(arr){
    return arr1.indexOf(arr) < 0;    // 此处对indexOf方法的参数略有不解，是直接传了一个数组当参数？
  });
  return arr2;
}

destroyer([1, 2, 3, 1, 2, 3], 2, 3);
```


我终于知道自己的错误在哪儿了，问题出在我对参数的理解上。函数 destroyer 的形式参数只有一个 arr ，而实际参数远多于此，但这并无影响， arr 依然只是代表第一个参数而已。

我错误地理解为 arr 的值为全部的参数集合，额，要是这样还要 arguments 干嘛。哇，被自己蠢哭了。

既然知道是这里出错了，再加上对 filter 的理解，那么这两种解法终于也都清晰明了啦。

对了，之所以能发现自己错在哪里，是因为我单单在 destroyer 函数体内 return 了一下 arr，经过几次测试后又重新拿起《js高级程序设计》翻看了一下参数的详细讲解。还是要好好地学习怎么检查和调试啊……

关灯睡觉。这么几道题，折腾了一天，我也是服了我自己。