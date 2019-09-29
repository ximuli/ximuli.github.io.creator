---
title: Cookie注册与登录
date: 2018-08-27
categories:
- 技术
tags: 
- JavaScript
---

# Cookie



## Cookie 是什么

1. Cookie 是浏览器访问服务器后，服务器传给浏览器的一段数据。

2. 浏览器需要保存这段数据，不得轻易删除。

3. 此后每次浏览器访问该服务器，都必须带上这段数据。

Cookie 就是这么简单，这就是 Web 开发里 Cookie 的含义。



## Cookie 的特点

1. 服务器通过 Set-Cookie 响应头设置 Cookie

```javascript
// node.js

response.setHeader('Set-Cookie','xxxxxx')
```

2. 浏览器得到 Cookie 之后，每次请求都要带上 Cookie
3. 服务器读取 Cookie 就知道登录用户的信息



## Cookie 的作用

Cookie 一般有两个作用。

第一个作用是识别用户身份。

第二个作用是记录历史。



## 相关问题

问：在 Chrome 登录了得到 Cookie，用 Safari 访问，Safari 会带上 Cookie 吗

no

问：Cookie 存在哪

Windows 存在 C 盘的一个文件里

问：Cookie会被用户篡改吗？

可以，Session 来解决这个问题，防止用户篡改

问：Cookie 有效期吗？

默认有效期20分钟左右，不同浏览器策略不同

后端可以强制设置有效期，具体语法看 MDN

问：Cookie 遵守同源策略吗？

有，不过跟 AJAX 的同源策略稍微有些不同。
当请求 qq.com 下的资源时，浏览器会默认带上 qq.com 对应的 Cookie，不会带上 baidu.com 对应的 Cookie

当请求 v.qq.com 下的资源时，浏览器不仅会带上 v.qq.com 的Cookie，还会带上 qq.com 的 Cookie
另外 Cookie 还可以根据路径做限制，请自行了解，这个功能用得比较少。



# 注册与登录



## 注册与登录的时候前后端都发生了什么？

注册：

1. 打开注册页面，输入信息，在点击注册的时候会发送一个 POST 请求，把输入的账号密码等资料都上传给 server

2. server 认为没有问题就把用户输入的信息写到数据库，之后告诉用户注册成功

登录：

1. 用户输入信息，点击登录会发送 POST 请求把信息传给 server

2. server 去看这个用户信息在不在数据库中，如果不在，那就告诉用户先去注册 

3. 如果用户信息存在于数据库中，说明用户注册过，这个时候 server 就设置一下 cookie ，把用户信息告知浏览器

4. 浏览器会把 cookie 记下来，当用户请求其他页面（GET 请求）的时候会带上这段 cookie 

5. server 发现请求中有 cookie 信息，就通过 cookie 里记录的信息去数据库找到相关用户，并拿到这个用户的其他信息

6. server 找到用户请求的页面，把用户的信息填入页面，然后响应回去

7. 用户就可以看到页面上有属于自己的信息  

小结： 

注册就是写数据库

登录就是去跟数据库做对比



（完）
