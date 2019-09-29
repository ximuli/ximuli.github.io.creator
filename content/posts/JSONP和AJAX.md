---
title: JSONP 和 AJAX
date: 2018-08-17
categories:
- 技术
tags: 
- JavaScript
---



>  首先我们应该明白，JSONP 和 JSON 没什么关系。



# JSON


全称 JavaScript Object Notation

是一种由道格拉斯·克罗克福特构想和设计、轻量级的数据交换语言。注意，这是一门语言。



# JSONP

## 什么是 JSONP ？

请求方：前端（浏览器）

响应方：后端（服务器）

请求方动态创建 script，将 src 指向响应方，同时传一个查询参数 ?callback=xxx

响应方根据查询参数 callback，构造形如 xxx.call(undefined, '你要的数据') 这样的响应

浏览器接收到响应，就会执行 xxx.call(undefined, '你要的数据')

那么请求方就知道了他要的数据

这就是 JSONP



## 关于 JSONP 的一些约定

1. callbackName -> callback
2. xxx -> 随机数 frank12312312312321325()
3. jQuery 用法
```javascript
$.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
 success: function( response ) {
     if(response === 'success'){
     amount.innerText = amount.innerText - 1
     }
 }
 })
```



## JSONP 为什么不支持 POST 请求？ 

1. JSONP 是通过动态创建 script 实现的
2. 创建 script 只能发送 GET ，没有办法发送 POST 。




# AJAX

异步的 JavaScript 和 XML （Asynchronous Javascript And XML）



## 什么是 AJAX

1. 使用 XMLHttpRequest 发请求
2. 服务器返回 XML 格式的字符串
3. JS 解析 XML ，并局部更新页面



## 原生 JS 写出一个 AJAX 请求

```javascript
let request = new XMLHttpRequest()
request.onreadystatechange = ()=> {
    if (request.readyState === 4) {
        console.log("请求和响应都完毕了")
        if (request.status >= 200 && request.status < 300) {
            console.log("请求成功")
            let string = request.responseText
            let object = window.JSON.parse(string)
        }
        else if (request.status >= 400) {
            console.log("请求失败")
        }
    }
}
request.open('GET', '/xxx')    //配置 request
request.send()
```


##  自己实现一个 jQuery.ajax

```javascript
window.jQuery = function(nodeOrSeletor) {
	let nodes = {}
	nodes.addClass = function () {}
	nodes.html = function () {}
	return nodes
}

window.$ = window.jQuery

window.jQuery.ajax = function({url,method,body,headers}) {
	return new Promise( function (resolve, reject) {  // Promise 本身来说只是为了规定一种形式
		let request = new XMLHttpRequest()
		request.open(method, url)
		for (let key in headers) {
	        let value = headers[key]
	        request.setRequestHeader(key, value) 	
	    }
		request.onreadystatechange = ()=> {
			if (request.readyState === 4) {
				console.log('请求和响应都完毕了。')
				if (request.status >= 200 && request.status < 300) {
					resolve.call(undefined, request.responseText)  //传过去一个参数。
				}
				else if (request.status >= 400) {
					reject.call(undefined, request)
				}
			}
		}
		request.send(body)
	} )
}

var btn = document.getElementById('btn')
btn.addEventListener('click', ()=>{
	window.jQuery.ajax({
		url:'/jewel',
		method:'POST',
		headers:{
			'content-type':'application/x-www-form-urlencoded',
			'jewel':'25'
		}
	}).then(
        (x)=>{console.log(x);console.log('成功')},
        (y)=>{console.log(y);console.log('失败')}
	)
})
```

[完整代码链接](https://github.com/ximuli/nodejs-test/blob/master/main.js)



# 同源策略

为了安全！

只有 协议+端口+域名 一模一样才允许发 AJAX 请求

1. http://baidu.com 可以向 http://www.baidu.com 发 AJAX 请求吗    no
2. http://baidu.com:80 可以向 http://baidu.com:81 发 AJAX 请求吗   no

浏览器必须保证：

只有 「协议+端口+域名」 一模一样才允许发 AJAX 请求

CORS 可以告诉浏览器，我俩一家的，别阻止它

CORS 全称：Cross-origin resource sharing   跨站资源共享

CORS 就是服务端在响应头里加了一段代码：

```javascript
// node.js
response.setHeader('Access-Control-Allow-Origin', 'http:/xxx.com:8008')
```


资料：

[ JSON 官网](http://json.org/)

[AJAX](http://javascript.ruanyifeng.com/bom/ajax.html)

[浏览器同源政策及其规避方法](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)

（完）