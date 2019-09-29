---
title: HTML 常见标签 
date: 2018-04-18
categories: 
- 技术
tags: 
- HTML
---

## 关于 a 标签和 button 标签

* 如果是要跳转到其他页面或某一部分，就用 a 标签；如果是想弹出对话框之类的操作，就用 button 标签。
* 二者的区别之一在于是否为 空标签 。





## 关于 CSS 布局

目前 CSS 布局最适合的布局只有两种：横向布局和纵向布局。所以在写 HTML 的时候要多注意一下，怎么写才是最方便继续写 CSS 的。



## iframe 标签

* 嵌套页面

* 默认存在边框，所以通常会直接设置属性 `frameborder = "0"` 来取消默认的边框样式

* 例如 `<iframe src="https://www.baidu.com" name="xxx" frameborder = "0"></iframe>`   

  name 属性指定当前 iframe 的名称；此时如果有另外的 a 标签属性是 `target=xxx`，那么此 a 标签链接被点击时网页会在名为 xxx 的 iframe 中打开。

* sandbox 属性


学习资料：

[Iframe 有什么好处，有什么坏处？](https://www.zhihu.com/question/20653055)

[iframe MDN]([https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe](https://developer.mozilla.og/zh-CN/docs/Web/HTML/Element/iframe)



## a 标签

跳转页面，发起 GET 请求

### target 属性

`target="_blank"` 在新窗口打开

`target="_self"` 在当前窗口打开

`target="_parent"` 在父级窗口打开 

`target="_top"`  在顶层窗口打开



### download 属性

此属性指示浏览器下载URL而不是导航到URL
```
<a href="http://qq.com" download>下载</a>
```

上面的例子点击 a 链接会下载 href 属性中的链接页面

注：如果 HTTP 响应的 Content-type: application/otcet-stream ，那么浏览器就会下载。



###  href 属性

如下例子：

```
<a href="qq.com"><a>
```

* 如果用以上形式想访问 qq.com 则会出错


* 必须加上 http:// 或者 https:// ；也可以直接 `<a href="//qq.com"><a>` ，表示继承当前页面的协议。

再来看一个例子：

```
<a href="?name=frank"><a>
```

* 不会报错，这样写很自然
* 会自动在当前页面添加上 href 属性里的一串字符并发起 get 请求

注：`<a href="#bottom"><a>`  类似这样的锚点链接并不会发起请求；` <a href="#><a>` 点击 a 标签返回页面顶部。



#### 伪协议的应用

```
<a href="javascript:;"><a>
```

此 a 标签点击后不会跳转。



## form 标签

跳转页面，发起 POST请求

```
<form action="" method="post">
  <input type="text" name="xxx">
  <input type="password" name="yyy">
  <input type="submit" value="提交">
</form>
```

注：

* 如果 form 里没有提交按钮，那么就无法提交此form，除非使用 js。
* method 制定请求类型，一般其值为 `post`。如果没有此属性，则默认提交 get 请求（但是这样做没有什么意义）。
  * 如果为 get ，则 name 属性值将以查询参数的形式出现 
* post请求下，name 属性的值都会体现在请求的第四部分当中；而且密码将会以明文显示
* form 也有 target 属性，作用和 a 标签相似。
* form 中的 input 标签只有带上 name 属性，在提交的时候其数据才会被提交



## button 标签

注：

* button 标签没有设置 type 属性时，会被默认为是 submit ，直接回车就会提交。
* 与 input 的区别就在于是否为 空元素。



## input 标签

### input 标签与 label 关联

```
<input type="checkbox" id="xxx"><label for="xxx">爱我</label>
```

关联后点击【爱我】也会勾选住复选框。

建立关联的另一种方法：

```
<label><input type="checkbox">爱我</label>
```

这种方式不用加 id 属性 和 for 属性来建立关联。老司机都这样写。

注：type 为其他属性时，这样的关联方法相同。



### type="checkbox"

```
<label><input type="checkbox" name="fruit" value="orange">orange</label>
<label><input type="checkbox" name="fruit" value="banana">banana</label>
```

name 值相同，复选框效果



### type="radio"

```
<label><input type="radio" name="loveme" value="yes">Yes</label>
<label><input type="radio" name="loveme" value="no">No</label>
```

name 值相同，才会有单选的效果

注：[select](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/select)



## table 标签

用于展示数据

th table head

tr table row

td table data

一个完整的 table 如下：

```
<table border=1>
  <colgroup>
    <col width=100></col>  
    <col bgcolor=red width=200></col>
    <col width=100></col>
    <col width=70></col>
  </colgroup>
  <thead>
    <tr>
      <th>项目</th><th>姓名</th><th>班级</th><th>分数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th></th><td>小明</td><td>1</td><td>94</td>
    </tr>
    <tr>
      <th></th><td>小红</td><td>2</td><td>96</td>
    </tr>
    <tr>
      <th>平均分</th><td></td><td></td><td>95</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th>总分</th><td></td><td></td><td>190</td>
    </tr>
  </tfoot>
</table>
```

注：table 的 border 默认是占据空间的，可以使用 css 属性 `border-collapse: collapse` 来合并边框。



（完）