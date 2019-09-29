---
title: ES6 系列：类
date: 2018-08-23
categories:
- 技术
tags: 
- JavaScript
---



# 原型

原型是啥：https://www.zhihu.com/question/56770432/answer/315342130

原型就是共有属性

JS 只用一个很简单的规则就实现了对象复用



# 类

类是啥？

![image](http://wx2.sinaimg.cn/mw690/d1b5fd6bly1fujyyk3h55j20r60h20ve.jpg)

依据上图我们来自己写个例子：

```
// 如何用原型模拟类

var 人类共有属性 = {
  walk() {
    console.log('走两步')
  },
  species: '人类'
}

function createPerson(name,age) {
  var obj = {}
  obj.name = name || ''
  obj.age = age || 18
  obj.__proto__ = 人类共有属性
  return obj
}

createPerson('jewel')
```

结果如下：

![image](http://wx1.sinaimg.cn/mw690/d1b5fd6bly1fujyynft4dj2062040t8i.jpg)



# ES 6 中的类

语法如下：

```
class Person {
  constructor(name,age) {
    this.name = name
    this.age = 18
  }
  walk() {
    console.log('走两步')
  }
}
```

`contructor` 里写的是自有属性，外写的是共有属性。我们可以新建一个对象来验证一下。

![image](http://wx3.sinaimg.cn/mw690/d1b5fd6bly1fujyyrivh8j2080093t8l.jpg)


更多的语法：

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    walk() {
        console.log('走两步')
    }
}
var p1 = new Person('jewel')
console.log(p1)
```
打印的结果如下：

![image](http://wx4.sinaimg.cn/mw690/d1b5fd6bly1fujyyun48ij209q0663yc.jpg)

回顾一下我们目前为止用到的关键字：

class 类

new 新建某个类的对象

constructor 每个类都需要有这个，用来构造自有属性

extends 一个类想继承一个类就用 extends

super 调用超类。把超类的自有属性继承过来。使用 this 之前必须调用 super()



## 属性封装

其实 ES 6 中关于 class 的语法还不健全，比如在共有属性区域我们只能使用函数，比如上面例子中的 `walk()` ，目前并不支持 `key: value` 之类的语法。

那如何达到使用属性的效果呢？

用原型可以轻松实现。

依然使用上个例子的代码：

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    walk() {
        console.log('走两步')
    }
}
var p1 = new Person('jewel')

p1.__proto__.种族 = '人类'

console.log(p1.种族)   // 人类
```

就目前而言 class 的语法做不到这一点。

但是我们可以近似地做到。

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
    race() {
        return '动物'
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    walk() {
        console.log('走两步')
    }
}
var p1 = new Person('jewel')
p1.race()  //动物
```

但是这样很不舒服。我明明只想要一个属性，却不得不一直加个括号来执行函数。

ES 6 支持在函数名称之前加个 **get** ，这样就不用加括号了。

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
    get race() {
        return '动物'
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    walk() {
        console.log('走两步')
    }
}
var p1 = new Person('jewel')
p1.race    //动物
```

那么问题来了，如果我们一时手贱写错了怎么办？除了直接改原始代码，是否能在后写的代码里来更改 get 之后的函数里的内容呢？

答案是并不能。

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
    get race() {
        return '运物'
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    walk() {
        console.log('走两步')
    }
}
var p1 = new Person('jewel')
console.log(p1.race)    //运物
p1.race = '动物'
console.log(p1.race)    //运物
```

改不动。ES 6 还提供了 **set** 。

我们需要一个隐藏的属性（现在的 JS 还没做到隐藏这个属性，还在开发当中…… 我们先骗一下自己这是隐藏的……），用来保存真正的值，然后用两个函数去操作这个隐藏的属性。

这个叫做属性封装。

```
class Animal {
    constructor() {
        this.body = '身体'
        this._race = '运物' //隐藏属性
    }
    move() {
        console.log('能动')
    }
    get race() {
        return this._race
    }
    set race(value) {
        this._race = value
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    walk() {
        console.log('走两步')
    }
}
var p1 = new Person('jewel')
console.log(p1.race)  //运物
p1.race = '动物'
console.log(p1.race)  //动物
```
这样我们既可以读又可以写了。



### 利用 get 来做点什么

有时候我们需要控制一下读写的权限。例如年龄不能随便改，应该设置成只读。

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this._age = 18
    }
    walk() {
        console.log('走两步')
    }
    get age() {
        return this._age
    }
}
var p1 = new Person('jewel')
```

这样年龄就没有权限改了。



### 利用 set 来做点什么

控制写

假如我们想改名字，但是不能随便改，只能改成两个字到四个字。

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this._name = name
        this._age = 18
    }
    walk() {
        console.log('走两步')
    }
    get age() {
        return this._age
    }
    get name() {
        return this._name
    }
    set name(v) {
        if ( v.length > 4 ) {
            console.log('不行')
        }
        else if ( v.length < 2 ) {
            console.log('不行')
        } 
        else {
            this._name = v
        }
    }
}
var p1 = new Person('王大锤')
```



## 静态方法

通过 class 的名字直接 `.` 出来

```
class Animal {
    constructor() {
        this.body = '身体'
    }
    move() {
        console.log('能动')
    }
}

class Person extends Animal {  //基类  超类
    constructor(name) {
        super()
        this.name = name
        this.age = 18
    }
    static die() {
        console.log('地球炸了')
    }
    walk() {
        console.log('走两步')
    }
}

Person.die()    //地球炸了 

```



## 其他

Species

Mix-ins

参看下方 MDN 链接。



# 总结

相对来说，目前的 JavaScript 中的 class 还并不是那么好用，但是预计以后 class 会发展的比原型好很多。

现在就慢慢学起来。以备后用。



资料：

[原型是啥](https://www.zhihu.com/question/56770432/answer/315342130)

[类-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)

（完）




