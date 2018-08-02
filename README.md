# 自底向上理解Git（Git: From the Bottom UP）

[TOC]

原文地址：[https://jwiegley.github.io/git-from-the-bottom-up/](https://jwiegley.github.io/git-from-the-bottom-up/)

本书GitBook地址：[https://legacy.gitbook.com/book/princewang1994/git-from-the-bottom-up/details](https://legacy.gitbook.com/book/princewang1994/git-from-the-bottom-up/details)

博客同步：http://blog.prince2015.club

## Motivation

​	Git是目前最流行的版本控制工具，从Git工具出发衍生出的软件开发，集成环境不计其数。然而对许多新入门的同学而言，Git繁多的选项和复杂的命令，给入门带来了一些困难。互联网上不乏Git的快速入门教程（如[廖雪峰老师的博客](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)），对于入门新手而言，在阅读完这些教程以后，完全可以完成一些Git的日常操作如Add，Commit，Push等操作，然而当更加复杂的命令，如Git的分支操作，暂存等等高级操作时，那些比较难懂的命令（如Reset和Rebase）就会带来不小的困难。在这个时候，从底层了解一些Git的设计思想和原理，能够帮助新人们快速了解Git的设计哲学，对于Gitter来说，也可以温故知新。

​	本文的原文是John Jwiegley的Git From the Bottom Up，是一篇非常好的Git原理性文章，通俗易懂，而且带有一些小例子，也是本人从入门Git有所提升的重要资料，然而在网上没有找到非常完善的中文版（如果找到的同学可以联系我），于是萌生了翻译中文版的想法。希望在学习和工作之余翻译这篇博客，联系一些文档的写法，也重新温习Git的知识，当然也希望能够帮助到一些刚入门Git的同学。

​	在翻译文法方面，由于本人英文水平有限，在措辞和整体翻译上可能难免有一些偏差，希望各位看官们见谅。整体上我会尽量直白的表达作者想表达的意思，但可能不会逐字逐句的直译，我更希望这篇文章能够在我的翻译下，能够有一些新的东西。

后续我也会增加一些Git的其他衍生材料和本人的一些理解

**版权声明：本文的翻译出于个人学习，不包含任何商业目的，如有侵犯作者权益，立即删除。**

## Content

### 1. Repository

* [Introduction](/Repository/introduction.md)
* [Repository: 目录内容追踪](/Repository/repository-directory-content-tracking.md)
* [Blob简介](/Repository/introducing-the-blob.md)
* 存储在Tree中的blob
* Tree是如何生成的
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

衍生阅读

## 联系我

如有任何对本书的意见或建议，欢迎随时联系我！以下是我的联系方式：

**E-mail**: princewang1994@gmail.com

**个人主页**：[http://blog.prince2015.club](http://blog.prince2015.club) 或 [http://princewang1994.github.io](http://princewang1994.github.io)，欢迎访问

