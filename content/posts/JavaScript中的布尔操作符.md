---
title: JavaScript中的布尔操作符
date: 2018-01-07
categories: 
- 技术
tags: 
- JavaScript
---

# 布尔操作符

## 逻辑非 ( ! )

逻辑非操作符可以应用于ECMAScript中的任何值。无论这个值是什么数据类型，这个操作符都会**返回一个布尔值**。 

逻辑非操作符首先会将它的操作数**转换为一个布尔值，然后再对其求反**。（ps：此处应该可以理解为先用 Boolean() 转型函数将操作数转换为布尔值，然后对其求反。 2018-1-7 ）

同时使用两个逻辑非操作符，就会模拟**Boolean()** 转型函数的行为。

## 逻辑与 ( && )、逻辑或( || )

这两者都属于**短路操作符** ，即：如果第一个操作数能够决定结果，那么就不会再对第二个操作数求值。

对于逻辑与操作符 ( && ) 而言，

如果第一个操作数是 false ，则无论第二个操作数是什么值，结果都必定是 false 。

逻辑与的真值表如下：

| 第一个操作数 | 第二个操作数 |  结果   |
| :----: | :----: | :---: |
|  ture  |  true  | true  |
|  true  | false  | false |
| false  |  true  | false |
| false  | false  | false |

逻辑与操作可以应用于任何类型的操作数，而不仅仅是布尔值。在有一个操作数不是布尔值的情况下，逻辑与操作就不一定返回布尔值；此时，它遵循如下规则：

* 如果第一个操作数是对象，则返回第二个操作数；
* 如果第二个操作数是对象，则只有在第一个操作数的求值结果为 true 的情况下才会返回该对象；
* 如果两个操作数都是对象，则返回第二个操作数；
* 如果第一个操作数是 null ，则返回 null ；
* 如果第一个操作数是 NaN ，则返回 NaN ；
* 如果第一个操作数是 undefined ，则返回 undefined 。



————————————————————*分割线* ——————————————————————



而相反地，对于逻辑或操作符 ( || ) 而言，

如果第一个操作数是 true ，那么就不会对第二个操作数求值，结果必定是 true 。

逻辑或的真值表：

| 第一个操作数 | 第二个操作数 |  结果   |
| :----: | :----: | :---: |
|  ture  |  true  | true  |
|  true  | false  | true  |
| false  |  true  | true  |
| false  | false  | false |

和逻辑与操作相似，如果有一个操作数不是布尔值，逻辑或也不一定返回布尔值；此时，它遵循如下规则：

* 如果第一个操作数是对象，则返回第一个操作数；
* 如果第一个操作数的求值结果为 false ，则返回第二个操作数；
* 如果两个操作数都是对象，则返回第一个操作数；
* 如果两个操作数都是 null ，则返回 null ；
* 如果两个操作数都是 NaN ，则返回 NaN ；
* 如果两个操作数都是 undefined ，则返回 undefined 。

利用逻辑或操作符可以避免为变量赋予 null 或 undefined 值。例如：

```javascript
var myObject = preferredObject || backupObject
```

（ps：可以把`backupObject`理解为 **默认值**）

