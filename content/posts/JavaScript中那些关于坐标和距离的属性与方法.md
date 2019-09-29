---
title: JavaScript中那些关于坐标和距离的属性与方法
date: 2019-05-26 21:23:03
categories:
- 技术
tags:
- JavaScript
---

# 一 前言

在前端开发中总会遇到各种各样需要使用或计算坐标和距离的情况，但是这些属性和方法众多，全部熟练地记下来并非是一件易事，大多只能现查，耗费不少时间精力，于是便有了整理记录的想法，即加深了印象，又方便随时查阅。

<!-- more -->

# 二 window 对象

> 浏览器里面，window 对象（注意，w为小写）指当前的浏览器窗口。
>
> 它也是当前页面的顶层对象，即最高一层的对象，所有其他对象都是它的下属。一个变量如果未声明，那么默认就是顶层对象的属性。
>
> 摘自《阮一峰 JavaScript 教程》

## 位置大小属性

### window.screenX , window.screenY

只读属性

返回浏览器窗口左上角相对于当前屏幕左上角的水平距离和垂直距离（单位像素）。

### window.innerHeight , window.innerWidth

只读属性

返回网页在当前窗口中可见区域的高度和宽度，即「视口」（viewport）的大小（单位像素）。

注意，这两个属性包括滚动条的高度和宽度。

### window.outerHeight , window.outerWidth

只读属性

返回浏览器窗口的高度和宽度，包括浏览器菜单和边框（单位像素）。

### window.scrollX , window.scrollY

只读属性

别名： window.pageXOffset , window.pageYOffset

分别返回页面的水平滚动距离和垂直滚动距离，单位都是像素。

> 注意，这两个属性的返回值不是整数，而是双精度浮点数。如果页面没有滚动，它们的值就是0。
>
> 摘自《阮一峰 JavaScript 教程》

> 为了跨浏览器兼容性，请使用 window.pageXOffset 代替 window.scrollX。另外，旧版本的 IE（<9）两个属性都不支持，必须通过其他的非标准属性来解决此问题。
>
> 摘自 MDN ：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/scrollX

## window 对象的方法

### window.scrollTo() , window.scroll() , window.scrollBy()

window.scrollTo 方法  ---> 别名： window.scroll 方法

> 用于将文档滚动到指定位置。
>
> 它接受两个参数，表示滚动后位于窗口左上角的页面坐标。

也可以接受一个配置对象作为参数。

```js
window.scrollTo(options)
```

配置对象 options 有三个属性。

* top：滚动后页面左上角的垂直坐标，即 y 坐标。
* left：滚动后页面左上角的水平坐标，即 x 坐标。
* behavior：字符串，表示滚动的方式，有三个可能值（smooth、instant、auto），默认值为 auto。

window.scrollBy 方法用于将网页滚动指定距离（单位像素）。

> 它接受两个参数：水平向右滚动的像素，垂直向下滚动的像素。

注意：仔细体会这两者的差别。

# 三 Element 节点

> Element节点对象对应网页的 HTML 元素。每一个 HTML 元素，在 DOM 树上都会转化成一个Element节点对象（简称元素节点）。

## 相关属性

### Element.clientHeight，Element.clientWidth

分别返回元素的高度和宽度，始终是整数值。

如果该元素是内联元素（`display: inline;`），则返回值为 0。

从盒模型的概念上来讲，返回的数值计算包括元素的 content 和 padding ，不包括 border 和 margin 。

如果有滚动条，返回的数值会减去滚动条占据的宽度或高度。（即不包含滚动条在内）

```js
// 浏览器视口高度
document.documentElement.clientHeight

// 网页总高度
document.body.clientHeight
```

### Element.clientLeft，Element.clientTop

分别返回元素的左边框宽度和上边框宽度，没有边框则返回 0。

同样不支持内联元素。

（我没太明白这两个属性有啥作用……）

### Element.scrollHeight，Element.scrollWidth

返回当前元素的总高度和总宽度，包括溢出容器、当前并不可见的部分。

包括 padding 区域。

包括伪元素的宽度和高度。

不包含滚动条的宽度和高度。

来个小 demo 辅助下理解：

```html
<div class="box"> 666 </div>
```
```css
.box {
  width: 200px; height: 200px; overflow: hidden;
  border: 1px solid red; padding: 10px; position: relative;
}
.box::after {
  position: absolute; content: '';
  width: 100px; height: 100px; left: 100%;
}
```
```js
let box = document.querySelector('.box')
console.log(box.scrollWidth) // 320
console.log(box.scrollHeight) // 220
```

可以看到 box 元素的 `scrollHeight` 是 220，这个和我们提到的「包括 padding 区域」相符合。

那 box 元素的 `scrollWidth` 为啥是 320 ？ 是因为伪元素的位置和宽度，虽然伪元素溢出被隐藏了，但是这个属性返回的数值依然包括它。

当然不仅仅包括它的宽度和高度，它所处的位置也会计算在内。

比如把伪元素的 css 改一下：
```css
.box::after {
  position: absolute; content: '';
  width: 100px; height: 100px;
  left: 120%; top: 120%;
}
```

现在你要不要猜一下 box 的 `scrollWidth` 和 `scrollHeight` 分别是多少？

### Element.scrollLeft，Element.scrollTop

可读写，设置该属性的值，会导致浏览器将当前元素自动滚动到相应的位置。

分别返回当前元素的水平滚动距离和垂直滚动距离。

对于那些没有滚动条的网页元素，这两个属性总是等于 0。

如果要查看整张网页的水平的和垂直的滚动距离，要从 document.documentElement 元素上读取。

```js
document.documentElement.scrollLeft
document.documentElement.scrollTop
```
### Element.offsetHeight，Element.offsetWidth

分别返回元素的高度和宽度，包括元素本身的高和宽、padding 和 border ，以及滚动条的高和宽。

如果元素的 display 为 none，则返回 0。

与 clientHeight 和 clientWidth 相比，我想这对属性用的更多一点，因为更多的时候我们需要获取的是元素的完整宽高。

### Element.offsetLeft，Element.offsetTop

返回当前元素左上角相对于 Element.offsetParent 节点的水平和垂直位移。

说到这个我们来了解下 Element.offsetParent：

> Element.offsetParent 属性返回最靠近当前元素的、并且 CSS 的 position 属性不等于 static 的上层元素。
>
> 如果该元素是不可见的（display属性为none），或者位置是固定的（position属性为fixed），则offsetParent属性返回null。
>
> 如果某个元素的所有上层节点的position属性都是static，则Element.offsetParent属性指向<body>元素。
>
> 摘自《阮一峰 JavaScript 教程》

## 相关方法

### Element.getBoundingClientRect()

返回一个对象，提供当前元素的大小、位置等信息。

我常用来它获取元素的宽高和坐标。

该对象有如下属性：

* width 
* height 
* x 元素左上角相对于 **视口** 的横坐标
* y
* left
* right
* top
* bottom 

> 由于元素相对于视口（viewport）的位置，会随着页面滚动变化，因此表示位置的四个属性值，都不是固定不变的。如果想得到绝对位置，可以将 left 属性加上 window.scrollX ， top 属性加上 window.scrollY。
>
> 摘自《阮一峰 JavaScript 教程》


# 四 鼠标事件

## MouseEvent 接口

```js
let event = new MouseEvent('click', {
    // ...
})
```

通过 `addEventListener` 添加的 `click` 事件所产生的事件对象也是 MouseEvent 实例。

```js
let box = document.querySelector('.box')

box.addEventListener('click', (e) => {
  console.log(e) // 事件对象
})
```

这个事件对象，也就是 MouseEvent 实例，有很多属性，这里来简单分析一下。

### MouseEvent.clientX 和 MouseEvent.clientY

只读属性

分别返回鼠标位置相对于 **浏览器窗口** 左上角的水平坐标和垂直坐标。（不受滚动距离的影响）

可以这样理解：

client 本来就是客户端的意思，web 中的客户端就是浏览器，那 clientX 和 clientY 自然就是相对于浏览器的位置了。

这两个属性还分别有一个别名 MouseEvent.x 和 MouseEvent.y 。

### MouseEvent.screenX，MouseEvent.screenY

只读属性

分别返回鼠标位置相对于 **屏幕（显示器屏幕区域）** 左上角的水平坐标和垂直坐标。

screen 是屏幕的意思，所以，你懂的。

### MouseEvent.offsetX，MouseEvent.offsetY

只读属性

分别返回鼠标位置相对于 **目标节点（即当前元素）** 左上角 **padding 边缘** 的 水平距离和垂直距离。

offset 有偏移的意思，所以这里也可以理解为鼠标位置相对于目标元素内部左上角的偏移值，和目标元素本身以及外部的元素都无关。

那 「padding 边缘」是什么意思呢？ 

我们拿图说话：

![offsetX 和 offsetY](http://imgs.hellofed.com/youdaoNote/offsetX.png)

上图中三个元素分别有红蓝绿三种边框来区分，红蓝边框宽度为 1px ， 绿边框为 30px 。每个元素都有 padding 值。具体代码如下：

```html
<!-- HTML -->
<body>
  <div class="parent">
    <div class="hello">Hello</div>
  </div>
</body>
```

```css
/* css */
body {
  border: 1px solid red; margin: 0; padding: 20px;
}
.parent {
  border: 1px solid blue; padding-top: 50px;
}
.hello {
  width: 100px; height: 100px; padding: 100px; border: 30px solid green;
}
```

我们给 hello 元素添加一个 click 时间监听函数：

```js
// js
let hello = document.querySelector('.hello')

hello.addEventListener('click', (e) => {
  console.log(e)
  console.log(e.offsetX)
  console.log(e.offsetY)
})

```

分别点击 hello 元素的绿色边框和空白区域，会发现前者的值为负数，后者的值为整数，且都是相对空白区域的左上角开始计算的。

这就是我们一开始提到的 「鼠标位置相对于 **目标节点（即当前元素）** 左上角 **padding 边缘** 的 水平距离和垂直距离」 这句话的意思。

### MouseEvent.pageX，MouseEvent.pageY

只读属性

分别返回鼠标位置相对于文档左上角的距离。（包括滚动距离）

### MouseEvent.movementX，MouseEvent.movementY

只读属性

返回当前位置与上一个 mousemove 事件之间的水平距离和垂直距离。

很明显这两个属性和 mousemove 事件肯定有着密切的关系，所以我们再了解一下 mousemove 事件：

> 当鼠标在一个节点内部移动时触发。当鼠标持续移动时，该事件会连续触发。为了避免性能问题，建议对该事件的监听函数做一些限定，比如限定一段时间内只能运行一次。

说到这个应该会牵扯到「节流」，暂不深入了。

这两个属性还是很有用的，我虽然没咋用过，不过目前想来可以用来判断鼠标的移动方向等。


参考链接：

[window 对象 - WangDoc.com](https://wangdoc.com/javascript/bom/window.html)

[Element 节点 - WangDoc.com](https://wangdoc.com/javascript/dom/element.html)

[鼠标事件 - WangDoc.com](https://wangdoc.com/javascript/events/mouse.html)

（完）