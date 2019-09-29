---
title: HTTP入门
date: 2018-04-14
categories: 
- 技术
tags: 
- HTTP
---

# WWW的发明

WWW（World Wide Web）是Tim Berners-Lee （李爵士）于1989年至1992年间发明。

主要的三个概念：

1. URI，（统一资源标识符：Uniform Resource Identifier）
2. HTTP（超文本传输协议HyperText Transfer Protocol），两个电脑间传输内容的协议
3. HTML （超级文本标记语言：HyperText Markup Language）



# URI 是什么

全称：Uniform Resource Identifier

URI 分为 URL 和 URN 

URL（统一资源定位符Uniform Resource Locator）

URN（统一资源名称Uniform Resource Name）

URL的组成：

```
https://www.baidu.com/s?wd=hello&rsv_spt=1#5

协议    https:// 
域名    www.baidu.com 
路径    /s
查询参数    ?wd=hello&rsv_spt=1
锚点    #5
```



# DNS

全称：域名系统 -- Domain Name System

* 输入域名
* 输出IP





# 请求

Server + Client + HTTP

* 浏览器负责发起请求
* 服务器在 80 端口接收请求
* 服务器负责返回内容（响应）
* 浏览器负责下载响应内容

HTTP的作用就是指导浏览器和服务器如何进行沟通。




## get 和 post

get  获取  （访问网页等）

post  上传  （输入登录、注册信息等）



## 请求示例

（在命令行使用 curl 命令）

命令行输入：

 ```
curl -s -v -H "Frank: xxx" -- "https://www.baidu.com"
 ```

观察结果。

**注：结果中 `>` 开头的是请求， `<` 开头的是响应。** 

请求的内容为：

```
> GET / HTTP/1.1
> Host: www.baidu.com
> User-Agent: curl/7.58.0
> Accept: */*
> Frank: xxx
>
```



命令行输入：

```
curl -X POST -s -v -H "Frank: xxx" -- "https://www.baidu.com"
```

观察结果。

请求的内容为：

```
> POST / HTTP/1.1
> Host: www.baidu.com
> User-Agent: curl/7.58.0
> Accept: */*
> Frank: xxx
>
```



命令行输入：

```
curl -X POST -d "1234567890" -s -v -H "Frank: xxx" -- "https://www.baidu.com"
```

观察结果。

请求的内容为：

```
> POST / HTTP/1.1
> Host: www.baidu.com
> User-Agent: curl/7.58.0
> Accept: */*
> Frank: xxx
> Content-Length: 10
> Content-Type: application/x-www-form-urlencoded
> 
> 1234567890
```



## 请求的格式

```
1 动词 路径 协议/版本
2 Key1: value1
2 Key2: value2
2 Key3: value3
2 Content-Type: application/x-www-form-urlencoded
2 Host: www.baidu.com
2 User-Agent: curl/7.54.0
3 
4 要上传的数据
```

注：

1. 请求最多包含四部分，最少包含三部分。（也就是说第四部分可以为空）
2. 第三部分永远都是一个回车（`\n`）
3. 动词有 GET   POST   PUT   PATCH   DELETE   HEAD   OPTIONS 等
4. 这里的路径包括「查询参数」，但不包括「锚点」
5. 如果你没有写路径，那么路径默认为 /
6. 第 2 部分中的 Content-Type 标注了第 4 部分的格式




# 用 Chrome 发请求

1. 打开 Network
2. 地址栏输入网址 （要写全，带协议）
3. 在 Network 点击，查看 request，点击「view source」
4. 点击「view source」
5. 点击「view source」
6. 点击「view source」
7. 终于点了？可以看到请求的前三部分了
8. 如果有请求的第四部分，那么在 FormData 或 Payload 里面可以看到




# 响应

以上发的三个请求，前两个请求的响应为：

```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
Connection: Keep-Alive
Content-Length: 2443
Content-Type: text/html
Date: Tue, 10 Oct 2017 09:14:05 GMT
Etag: "5886041d-98b"
Last-Modified: Mon, 23 Jan 2017 13:24:45 GMT
Pragma: no-cache
Server: bfe/1.0.8.18
Set-Cookie: BDORZ=27315; max-age=86400; domain=.baidu.com; path=/

<!DOCTYPE html>
<!--STATUS OK--><html> <head> 后面太长，省略了……
```



```
HTTP/1.1 302 Found
Connection: Keep-Alive
Content-Length: 17931
Content-Type: text/html
Date: Tue, 10 Oct 2017 09:19:47 GMT
Etag: "54d9749e-460b"
Server: bfe/1.0.8.18

<html>
<head>
<meta http-equiv="content-type" content="text/html;charset=utf-8"> 后面太长，省略了……
```



1. GET 请求和 POST 请求对应的响应可以一样，也可以不一样
2. 响应的第四部分可以很长很长很长



响应的格式：

```
1 协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value2
2 Content-Length: 17931
2 Content-Type: text/html
3
4 要下载的内容

```

- 状态码要背，是服务器对浏览器说的话
  - 1xx 不常用
  - 2xx 表示成功（常见：200 普通成功 -- GET ， 204 创建成功 --  POST）
  - 3xx 表示滚吧  （常见：301、302、304）
  - 4xx 表示你丫错了 （访问错误，常见：404）
  - 5xx 表示好吧，我错了 （服务器错误）
- 状态解释没什么用
- 第 2 部分中的 Content-Type 标注了第 4 部分的格式
- 第 2 部分中的 Content-Type 遵循 MIME 规范 （标注了第四部分的格式）




注：以上的请求和响应内容及格式解读是在 mac os 环境下，我本人用 windows git bash 试验的时候，只有第四部分显示及文件内容显示位置稍有不同。



# 用 Chrome 查看响应

1. 打开 Network
2. 输入网址并回车
3. 选中第一个响应
4. 查看 Response Headers，点击「view source」，点击「view source」，点击「view source」
5. 你会看到响应的前两部分
6. 查看 Response 或者 Preview，你会看到响应的第 4 部分




学习资源：

[HTTP response codes - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)

[HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)

（完）