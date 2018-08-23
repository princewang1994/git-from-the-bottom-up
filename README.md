# 自底向上理解Git（Git: From the Bottom UP）

[TOC]

原文地址：[https://jwiegley.github.io/git-from-the-bottom-up/](https://jwiegley.github.io/git-from-the-bottom-up/)

本书GitBook地址：[https://legacy.gitbook.com/book/princewang1994/git-from-the-bottom-up/details](https://legacy.gitbook.com/book/princewang1994/git-from-the-bottom-up/details)

博客同步：http://blog.prince2015.club

## Motivation

Git是目前最流行的版本控制工具，从Git工具出发衍生出的软件开发，集成环境不计其数。然而对许多新入门的同学而言，Git繁多的选项和复杂的命令，给入门带来了一些困难。互联网上不乏Git的快速入门教程（如[廖雪峰老师的博客](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)），对于入门新手而言，在阅读完这些教程以后，完全可以完成一些Git的日常操作如Add，Commit，Push等操作，然而当更加复杂的命令，如Git的分支操作，暂存等等高级操作时，那些比较难懂的命令（如Reset和Rebase）就会带来不小的困难。在这个时候，从底层了解一些Git的设计思想和原理，能够帮助新人们快速了解Git的设计哲学，对于Gitter来说，也可以温故知新。

本文的原文是John Jwiegley的Git From the Bottom Up，是一篇非常好的Git原理性文章，通俗易懂，而且带有一些小例子，也是本人从入门Git有所提升的重要资料，然而在网上没有找到非常完善的中文版（如果找到的同学可以联系我），于是萌生了翻译中文版的想法。希望在学习和工作之余翻译这篇博客，联系一些文档的写法，也重新温习Git的知识，当然也希望能够帮助到一些刚入门Git的同学。

在翻译文法方面，由于本人英文水平有限，在措辞和整体翻译上可能难免有一些偏差，希望各位看官们见谅。整体上我会尽量直白的表达作者想表达的意思，但可能不会逐字逐句的直译，我更希望这篇文章能够在我的翻译下，能够有一些新的东西。后续我也会增加一些Git的其他衍生材料和本人的一些理解。

**版权声明：本文的翻译已经经过作者同意，但翻译完全出于个人学习和交流，不包含任何商业目的，如有侵犯作者权益，立即删除**

## 面向的读者

本文不是Git的科普文章，而是针对有一些基本Git知识，并能使用Git完成一些基本操作（如提交，推送，拉取等）的读者，对于完全零基础的读者，可以先通过上面提到的零基础教程来熟悉Git的基本用法，再读本文，一定会获益匪浅。另外，本文的行文思路清晰，文中例子丰富，在阅读过程中，跟随作者一起操作，能够更加深刻的理解Git的原理。

## 目录

### 1. Repository

* [引言](/Repository/introduction.md)
* [Repository: 目录内容追踪](/Repository/repository-directory-content-tracking.md)
* [Blob简介](/Repository/introducing-the-blob.md)
* [存储在Tree中的blob](/Repository/blobs-are-stored-in-trees.md)
* [Tree是如何生成的](/Repository/how-trees-are-made.md)
* 优美的提交（Commit）
* Commit的其他表示方法
* 分支与Rebase的力量
* 迭代式Rebase

### 2. 索引（The Index）

* 作为中间人的Index
* 更深入理解Index

### 3. 重置（Reset）

* 重置与否？是个问题
* 混合重置
* 软重置（Soft Reset）
* 硬重置（Hard Reset）

### 4. 暂存（Stashing）与 引用日志（reflog）

* 暂存（Stashing）与 引用日志（reflog）

### 5. 总结

* 总结

### 6. 延伸阅读

- [图解Git](https://marklodato.github.io/visual-git-guide/index-zh-cn.html)
- [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## 中英对照表



## 更新日志

- 2018.07.31: README.md初稿完成，Gitbook项目SUMMARY.md完成，项目基本结构搭建，后续准备补充
- 2018.08.01: 完成Introduction翻译
- 2018.08.02: 完成"Repository: 目录内容追踪"翻译
- 2018.08.03: Blob简介初稿翻译
- 2018.08.07: How trees are made上半篇翻译
- 2018.08.24: How trees are made下半篇翻译

## 联系我

如有任何对本书的意见或建议，欢迎随时联系我！以下是我的联系方式：

**E-mail**: princewang1994@gmail.com

**个人主页**：[http://blog.prince2015.club](http://blog.prince2015.club) 或 [http://princewang1994.github.io](http://princewang1994.github.io)，欢迎访问

