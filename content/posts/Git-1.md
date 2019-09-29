---
title: Git入门（1）
date: 2018-04-09
update: 2018-04-10
categories: 
- 技术
tags: 
- Git
---

>学习 Git 最好是在使用中学习，否则很难理解一些命令是什么意思。最好的学习方法就是，照着教程把命令挨个儿敲一遍，从实践中去理解和学习。

下面就开始今天的学习：

1. 创建目录作为项目目录：`mkdir git-demo-1`

2. 进入目录：`cd git-demo-1`

3. `git init` 这句命令意义在于把当前目录初始化为 Git 管理的仓库，可以理解为本地仓库初始化。之后当前位置路径后面会多出一个 `(master)` 的标识。

4. `ls -la` 就会看到 .git 目录，忽略它。（假装这句不存在）

5. 在 git-demo-1 目录中添加任意文件

   * `touch index.html`
   * `mkdir css`
   * `touch css/style.css`

6. 运行 `git status -sb` 可以看到文件前面有 ?? 号

   ```
   ## No commits yet on master
   ?? css/
   ?? index.html
   ```

   这些 ?? 表示 git 目前还不知道你要怎么对待这些变动

7. 使用 `git add` 将文件添加到 「暂存区」

   * 可以一个个分别添加
     * `git add index.html`
     * `git add css/style.css`
   * 也可以一次性添加
     * `git add .`   此命令意思是把当前目录（ `. ` 表示当前目录）里面的变动都添加到「暂存区」

8. 再次运行 `git status -sb`

   ```
   ## No commits yet on master
   A  css/style.css
   A  index.html
   ```

   A 的意思是添加，这里的意思是告诉 git ，你要将这些文件的变动添加到仓库里 

9. 使用 `git commit -m "一些描述"` 将 add 过的内容「正式提交」到本地仓库，并添加一些描述信息，方便以后查阅

   * 可以一个个 commit
     * `git commit index.html -m "添加index.html" `
     * `git commit css/style.css -m "添加 css/style.css"`
   * 也可以一次性 commit 
     * `git commit . -m "添加了几个文件"`

10. 再次运行 `git status -sb` ，发现没有文件变动了，这是因为变动都已经记录在仓库里了。

11. 使用 `git log` 可以看到历史上的变动

   ```
   commit 8e97dc4f7d45de99630273fcaee97477ab4db5e9 (HEAD -> master)
   Author: ximuli <ximuli666@163.com>
   Date:   Tue Apr 10 20:41:46 2018 +0800
   ```

12. 以上就是 git add / git commit 的一次完整过程




总结：

1. git init

   把当前目录变成 Git 可以管理的仓库。（初始化本地仓库）

2. git add

   在当前目录下各种操作：创建、修改文件、目录等等，然后使用 `git add 文件名/文件路径` ，表示把文件变动添加到「暂存区」。

3. git commit -m "一些描述"

   表示把文件变动正式提交到仓库；`-m` 后面输入的是本次提交的说明，可以输入任何内容，最好是可读的、有意义的，这样就可以方便地从历史记录里找到改动记录。 

4. git status -sb

   显示当前所有文件的状态。-s 的意思是显示总结（summary），-b 的意思是显示分支（branch）。

5. git log

   查看变更历史

6. 如果有新的变动，请依次执行 `git add xxx` 和 `git commit -m "xxx"`。



参考：

[廖雪峰的官方网站](https://www.liaoxuefeng.com/)

[饥人谷 -- 写代码啦](https://xiedaimala.com/)



疑问：`git commit -v`  

解答：-v 后命令行会以 vim 的形式把所做的变动都展示出来，同时相比 -m ，-v 也可以写更多更加具体的描述。



（完）