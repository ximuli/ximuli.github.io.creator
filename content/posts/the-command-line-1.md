---
title: 命令行基础
date: 2018-04-12
categories: 
- 技术
tags: 
- 命令行

---

# 一些基本概念

1. 文件与目录（文件夹）
2. `~`  `/`  `.`  `..`  `$` 
   - `~` 当前用户目录
   - `/` 硬盘（Linux下没有盘符的概念，`/` 就表示所有硬盘）
   - `.` 当前目录
   - `..` 父目录
   - `$` 没有实际意义，只是提醒你可以输入命令了

# 命令一般都是英文缩写

> 在windows中请安装使用 git bash

| 命令含义   | 英文               | 命令    |
| ------ | ---------------- | ----- |
| 创建目录   | make directory   | mkdir |
| 删除     | remove           | rm    |
| 移动、重命名 | move             | mv    |
| 复制     | copy             | cp    |
| 罗列     | list             | ls    |
| 改变目录   | change directory | cd    |



## 开始动手

1. `cd ~/Desktop` 进入桌面
2. `mkdir demo-1` 创建目录，这时你可以切到桌面，看到 demo-1 目录
3. `rm -rf demo-1` 删除目录
4. `touch 1.txt` 创建文件，如果你发现文件后缀不见了，请让该死的 Windows 显示文件后缀
5. `mv 1.txt 2.txt` 这样我们就把 1.txt 移到 2.txt 了，也就是重命名

# 常用命令

| 操作       | 命令                                       |
| -------- | ---------------------------------------- |
| 进入目录     | cd                                       |
| 显示当前目录   | pwd                                      |
| 创建目录     | mkdir 目录名                                |
| 创建目录     | mkdir -p 目录路径                            |
| 我是谁      | whoami                                   |
| --       | --                                       |
| 查看路径     | ls 路径                                    |
| 查看路径     | ls -a 路径                                 |
| 查看路径     | ls -l 路径                                 |
| 查看路径     | ls -al 路径                                |
| --       | --                                       |
| 创建文件     | echo '1' > 文件路径                          |
| 强制创建文件   | echo '1' >! 文件路径                         |
| 追加文件内容   | echo '1' >> 文件路径                         |
| 创建文件     | touch 文件名                                |
| 改变文件更新时间 | touch 文件名                                |
| --       | --                                       |
| 复制文件     | cp 源路径 目标路径                              |
| 复制目录     | cp -r 源路径 目标路径                           |
| --       | --                                       |
| 移动节点     | mv 源路径 目标路径                              |
| --       | --                                       |
| 删除文件     | rm 文件路径                                  |
| 强制删除文件   | rm -f 文件路径                               |
| 删除目录     | rm -r 目录路径                               |
| 强制删除目录   | rm -rf 目录路径                              |
| --       | --                                       |
| 查看目录结构   | tree                                     |
| 建立软链接    | ln -s 真实文件 链接                            |
| --       | --                                       |
| 下载文件     | curl -L [https://www.baidu.com](https://www.baidu.com/) > baidu.html |
| 拷贝网页     | wget -p -H -e robots=off [https://www.baidu.com](https://www.baidu.com/) |
| 磁盘占用     | df -kh                                   |
| 当前目录大小   | du -sh .                                 |
| 各文件大小    | du -h                                    |

学习最好的方法就是把这些命令挨个儿敲一遍。

> 注意：mkdir 目录名  和  mkdir -p 目录路径。
>
> 例如 `mkdir demo1/demo2/demo3` ，带不带引号都可以 。但是如果其中有特殊字符，则必须加引号。



# 推荐一个网站[explainshell](https://explainshell.com/)

它可以帮助你学习和理解命令的含义

- 在搜索框直接输入你想查询的命令，然后点击 EXPLAIN 按钮

# 关于vim

> vim 被誉为[编辑器之神](https://upclinux.github.io/intro/07/vim-and-emacs/)

## 如何学习

入门 vim 的三个推荐教程：

1. 在命令行输入 vimtutor
2. [简明 vim 练级攻略](https://coolshell.cn/articles/5426.html)
3. [一个 vim 游戏](https://vim-adventures.com/)

## 如何退出 vim

- 强制退出（不保存）：输入 `:q!` 然后回车
- 保存后退出： 输入 `:wq` 然后回车