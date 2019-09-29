---
title: JavaScript里的数据类型
date: 2018-05-14
categories: 
- 技术
tags: 
- JavaScript
---

# JS里的数据类型

## number

1. 二进制：0b 开头
2. 八进制：0开头
3. 十六进制：0x 开头





## string

1. 单引号和双引号
2. 空字符串和空格字符串
3. 转义， ` var a = '\'' ` 
4.  多行字符串

```javascript
var a = '12345\
67890'
a  //"1234567890"
//如果斜杠后面有空格，则会报错

//推荐：
var b = '12345' + 
'67890'
b  //"1234567890"

//ES6新语法
var c = `12345
67890`
c 
/*
"12345
67890"
*/
c.length  // 11 (因为有回车)
```



## undefined 和 null

1. 变量没有赋值，则为 undefined
2. 有一个对象 object，但是现在还不想给值，就可以设置为 null，表示 空对象





## object

1. 即为哈希表
2. 复杂类型，由简单类型组成
3.  key 其实是字符串，可以省略；但是某些情况下不可以省略，比如有一些特殊字符，或者以数字开头
4. 可以使用 delete 来删除对象中的键值对

```javascript
var person = {
  name: 'Jonathan',
  age: 18
}
delete person.name    // true
person.name    //undefined
'name' in person    //false
```

5.  for ... in ... 

```javascript
var person = {
  name: 'Jonathan',
  age: 18
}
for (var key in person) {
  console.log(key, person[key])  //注意，这里如果写成 person.key 则会产生歧义
}
//name Jonathan
//age 18
```



## typeof 操作符

```javascript
typeof null //'object'

function fn() {}
typeof fn  // 'function'
```



（完）



