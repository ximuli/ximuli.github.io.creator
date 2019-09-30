---
title: Sass学习笔记
date: 2017-01-23
categories: 
- 技术
tags: 
- Sass

---
> 这里是Jonathan的Sass学习笔记，**本笔记所有操作均在windows环境下进行 ，将持续更新**。

<!-- more -->

# 安装

## 1、通过命令安装 Sass 
先在电脑中安装好 **Ruby**  之后，接下来就可以安装 Sass 了。在windows下安装 Sass 有多种方法。但这几种方法都是非常的简单，只需要在命令终端输入一行命令即可。

打开电脑的命令终端，输入下面的命令：

`gem install sass`

如果上面的方法没有安装成功，可以使用下面的两种方法。

##  2、本地安装 Sass 

直接使用上面的命令安装会让你无法正常实现安装（网络受限原因），当碰到这种情况之时，那么安装需要特殊去处理，可以通过下面的方法来实现 Sass 的正常安装：

可以到 [Rubygems](http://rubygems.org/)(http://rubygems.org/) 网站上将 [Sass 的安装包](http://rubygems.org/gems/sass)（http://rubygems.org/gems/sass）下载下来，然后在命令终端输入：

`gem install` <把下载的安装包拖到这里>

直接回车即可安装成功。

注：在 iOSX 系统平台，可以直接将下载的安装包拖到 "gem install" 后面，如果在是 Windows 系统，需要手功输入安装的文件路径。

##  3、淘宝 RubyGems 镜像安装 Sass 

除了下载 Sass 安装包到本地安装之外，碰到网络原因无法安装时还可以使用淘宝 RubyGems 镜像安装 Sass。只是我们需要通过 gem sources 命令来配置源，先移除默认的 https://rubygems.org 源，然后添加淘宝的源 https://ruby.taobao.org：

第一步：移动默认的源

gem sources --remove https://rubygems.org/

第二步：指定淘宝的源

gem sources -a https://ruby.taobao.org/

第三步：查看指定的源是不是淘宝源

gem sources -l

返回结果如下：

*** CURRENT SOURCES ***https://ruby.taobao.org

请确保只有 ruby.taobao.org。如果无误之后，执行下面的命令：

gem install sass

#  更新和卸载Sass  

`gem update sass`

卸载： `gem uninstall sass`

#  Sass编译  

此处应查看更多的资料，另外，**调试** 也是需要注意的问题。

Sass 的编译。因为 Sass 开发之后，要让 Web 页面能调用 Sass 写好的东西，就得有一个过程，这个过程就称之为 Sass 编译过程。Sass 的编译有多种方法：

- 命令编译
- GUI工具编译
- 自动化编译

疑问：  前端自动化？？？ **Grunt 和 Gulp**      

#  Sass 常见编译错误  

在编译 Sass 代码时常会碰到一些错误，让编译失败。这样的错误有系统造成的也有人为造成的，但大部分都是人为过失引起编译失败。

**最为常见的一个错误就是字符编译引起的。** 在Sass的编译的过程中，是不是支持“GBK”编码的。所以在创建 Sass 文件时，就需要将文件编码设置为**“utf-8”**。

**另外一个错误就是路径中的中文字符引起的。** 所以在项目中文件命名或者文件目录命名**不要使用中文字符** 。而至于人为失误造成的编译失败，在编译过程中都会有具体的说明，大家可以根据编译器提供的错误信息进行对应的修改。

#  什么时候声明变量？ 

创建变量只适用于感觉确有必要的情况下。不要为了某些骇客行为而声明新变量，这丝毫没有作用。只有满足所有下述标准时方可创建新变量：

1. 该值至少重复出现了两次；
2. 该值至少可能会被更新一次；
3. 该值所有的表现都与变量有关（非巧合）。

基本上，没有理由声明一个永远不需要更新或者只在单一地方使用变量。

# 持续更新……